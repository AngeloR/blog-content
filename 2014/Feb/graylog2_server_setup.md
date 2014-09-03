# API Logging with Graylog2 -  Server Setup

> This is a two-part piece. Normally, I try and stay away from these, but the setup process can be a little long. The second piece will go live tomorrow and will contain information about how to interact with the system that you set up.

I recently hit a rather interesting problem and I thought I'd share some researching around the matter. I was tasked with a simple feature: 
<blockquote>Add additional metrics to an API logging mechanism</blockquote>

While it sounds simple enough, the additional metrics would cause our current table structure (logging in MySQL) some issues adding tons of rows and causing our api logging table to grow quite extensively. We were worried, to the point of unusability. So, as often happens when a developer is tasked with a "simple" task - the quick feature billowed into a rather monstrous task. 

How do we overhaul our current logging infrastructure so that we can:
1. Add the new metrics that we want to track
2. Don't ever run into this issue again


After a bit of thought, we decided to spent the time working on our API logging system with the idea that we can roll out more logging to the rest of the site. Instead of just cobbling something together using our MySQL instance we decided to move our logging infrastrucutre to something a little more robust - namely [Graylog2](http://graylog2.org/).

> Before we go any further I just want to point out that this tutorial is NOT for getting a production ready variant of Graylog2 running. There is a LOT more configuration that should go into getting this running in a production environment. This is exclusively a local testing environment to see what all the hubbub with Graylog2 is about.

## Graylog2
If you've never heard of Graylog2  think you better be prepared to have your socks knocked off. 

### Installation
The installation for Graylog2 is a little more invovled if you've only been used to getting lamp/lemp stacks running. There's config files that need configuring, applications that need installing and even a bit of finger-crossing. To make things a little easier for myself, I've opted to do the full Graylog2 install in a Vagrant VM. If you've never used Vagrant before, I recommend you check it out - it's very easy to get started with. 

#### Step 1: Oracle JRE
If you get to this point and you're going to argue with me over the Oracle JRE vs Open-jdk then just use what you'd like. To be honest I couldn't care less, and I don't know either of the following apps will either. The only reason I'm installing Oracle Java is because out of the two I'd rather go with the official Java for something like this.

This is super easy thanks to the webupd8team's ppa. 

```bash
sudo add-apt-repository ppa:webupd8team/java
sudo apt-get update
sudo apt-get install oracle-java7-installer
```

If you get an error saying that "add-apt-repository" is not a valid command, just install the python-software-properties and software-properties-common . Then go back and add the repo.

```bash
sudo apt-get install python-software-properties software-properties-common
```

The Java installer will take a bit of time to get through, and during it you'll have to accept a couple license agreements to continue. 


#### Step 2: Grab MongoDB
Installing MongoDB is pretty simple, especially considering the Mongo team gives us an official repo. They have full instructions for this at this url: http://docs.mongodb.org/manual/tutorial/install-mongodb-on-debian/

#### Step 3: Elasticsearch
Once you have Java set up, you'll want to download the right version of Elasticsearch. Graylog2 relies on Elasticsearch but it requires a very specific version of it. If you have the wrong version, nothing will work and you'll end up with errors about Graylog2 not being able to read the entire message. It's a confusing error but it has to do with the way Graylog2 and Elasticsearch exchange information. 

For this little walkthrough, I'm setting up the latest stable version of the Graylog2 server version 0.20.1 - This requires version 0.90.10 of Elasticsearch so go ahead and do the following

```bash
wget https://download.elasticsearch.org/elasticsearch/elasticsearch/elasticsearch-0.90.10.tar.gz
tar zxf elasticsearch-0.90.10.tar.gz
cd elasticsearch-0.90.10
```

Now you'll want to edit the Elasticsearch config file located here: `config/elasticsearch.yml`.

You'll want to configure as followed:
```bash
cluster.name: elasticsearch
transport.tcp.port: 9300
http.port: 9200
```

These are just the default settings, I've just uncommented them in the configuration file by deleting the `#`

Once that's done you can start up elastic search by running 

```bash
./bin-elasticsearch -f
```

#### Step 4: Graylog2-server
Next you'll need to grab the Graylog2-server component. This is what actually handles the logging mechanism. Below, we'll download the version of the server we want, extract the tar.gz and move into that directory. Then we'll simply copy over the Graylog configuration file to its appropraite place and then pop in to edit it.

```bash
wget https://github.com/Graylog2/graylog2-server/releases/download/0.20.1/graylog2-server-0.20.1.tgz
tar zxf graylog2-server-0.20.1.tgz
cd graylog2-server-0.20.1
sudo cp graylog2.conf.example /etc/graylog2.conf
sudo vim /etc/graylog2.conf
```

All we realy want to do here is confiugre the `password_secret` which is a salt that we'll be using to hash passwords. The configuration file has an example setup you can do to generate a salt. 

Next we want to set the root_password_sha2 hash. This again, is pretty straight forward, and the configuration file shows you how to do this in the comments right above where you'd be setting these values.

Next you'll want to scroll down to line 70 and uncomment the `elasticsearch_cluster_name` and ensure that it is set to `elasticsearch` (or something else if you changed the name of the cluster in the elasticsearch.yml file. 

With that done it's time to start up the Graylog2 server for the first time! Graylog recommends that you start it as follows the first time :

```bash
sudo java -jar graylog2-server.jar --debug
```

Eventually you'll see a line saying that it started and is not doing anything. At this point you can kill it and use the start script `./bin/graylog2ctl start`

#### Step 5: Graylog2-webserver
Finally is the pretty sweet Graylog2 webserver. This actually lets us configure the inputs on the server and allows us to actually SEE the data that we're logging. 

```bash
wget https://github.com/Graylog2/graylog2-web-interface/releases/download/0.20.1/graylog2-web-interface-0.20.1.tgz
tar zxf graylog2-web-interface-0.20.1.tgz
cd graylog2-web-interface-0.20.1
vim conf/graylog2-web-interface.conf
```

At this point, we've been working entirely from our local server with a single instance of elasticsearch running. So our `graylog2-server-uris` should be set to `http://127.0.0.1:12900`.

Then you just need to set an `application.secret`, which is just a random salt that will be used for crypto functions.

Now you just need to start the server!
```bash
./bin/graylog2-web-interface
```

If all goes well, you should see a `Listening for HTTP` message and a port which is where the web-server is running. Now just point your browser over to http://localhost:9000 and log in with the credentials `admin` and the password being whatever you configured during your graylog2 server setup. 

Take a look around the interface and under `System/Inputs` (http://localhost:9000/system/inputs) you'll want to add a new `GELF/UDP` Input. You can leave the defaults as is, and just give it a name so you know what it is. 

With that done, you are now ready to start logging to your Graylog2 server with their GELF protocol.

In the next part, I'll cover how you can start logging to your Graylog2 instance over PHP.)
