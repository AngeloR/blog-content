#Twemproxy: An Intro for Redis
A few years ago Twitter released a proxy they had written for memcache and redis. And I've recently gotten a chance to play with it. 

### Why should I care about Twemproxy?
Twemproxy (two-em-proxy) functions as a way to reduce the number of connections that you are making to a redis instance. But it also provides a built in sharding system allowing you some pretty awesome sharding control on-the-fly. 

Imagine this scenario:
1. You have an API written in Node.js that is clustered across your cores. We'll say you have 4 cores. That's 4 Node.js workers. 
2. You have 4 redis instances running on another host, with 4 cores. 
3. You have two redis hosts running (2 hosts, 4 cores each, each host running 4 redis instances). Your data is sharded across hosts.


In this case, each node host, which has 4 workers (w) each,  needs to be connected to each redis instance(r) running on each host (h). 

4w*(4r*2h) = 32

That's right. With one API host, running 4 workers, we have 32 connections assuming 1 connection per worker at a time. Not too bad to start. However, lets imagine that our little company starts doing REALLY awesome. We now have 10 redis hosts, and 5 api servers.

(4w*5h)*(4r*10h) = 800

Still not too bad right? Although, keep in mind, that's assuming that we only have one connection/worker. Realisically, if we're getting to this stage, there's a good chance that our api is using a heck of a lot more connections than that. 

With Twemproxy, we'd introduce redis request pipelining AND nullify the number of API hosts entirely. 

But more importantly, as our data grows we can take advantage of twemproxyies sharding and grouping capabilities to move data between our various redis shards. Right now we've been assuming even load across each redis instance on a host - but if one is more important than the others, it might make sense to spin up a bunch more of those instances. Twemproxy will allow us to simply add the new servers to its proxy list and intelligently direct the necessary traffic where it needs to go.

So with Twemproxy, you'd get: 

- Persistent server connections.
- Low connection count on cache servers.
- Pipelining of requests and responses.
- Proxying to multiple servers.
- Support for multiple server pools simultaneously.
- Automatic data sharding across multiple servers.
- Multiple hashing modes including consistent hashing and distribution.
- Auto-ejection of failure

And of course, it's pretty friggin fast. Not to mention that [antirez](http://antirez.com/news/44) has a few good things to say about it in conjunction with Redis.

### Getting it going
Hopefully, by now, I've at least convinced you that Twemproxy is worth a look. It has a pretty standard config/install process and if you're not familiar with compiling software, they've got a little walkthrough for you over on the [Twemproxy GitHub](https://github.com/twitter/twemproxy).

So, lets get this going shall we? Just a note, for whatever reason, even though it's called Twemproxy by everyone, it refers to itself as nutcracker. So once installed, don't try looking for the "twemproxy" command. You're really looking for "nutcracker".

wget https://twemproxy.googlecode.com/files/nutcracker
-0.3.0.tar.gz
tar zxvf nutcracker-0.3.0.tar.gz
cd nutcracker-0.3.0
CFLAGS="-ggdb3 -O0" ./configure --enable-debug=full
make
sudo make install

Before you can actually run it though, you'll need to spend some time creating a configuration file. They've included a sample in `conf/nutcracker.yml` but you'll need to change pretty much everything about it. 

For our scenario, you can just plug in the following, which we will customize for your setup.

alpha:
listen: 127.0.0.1:22121
hash: fnv1a_64
distribution: ketama
auto_eject_hosts: true
redis: true
server_retry_timeout: 2000
servers:
- 127.0.0.1:6379:1 server1-1
- 127.0.0.1:6380:1 server1-2


This configuration file defines a pool that we call "alpha". The name is pretty much arbitrary. The configuration file explanation is as follows:

1. We are going to listen locally on port 22121 for all redis connections to the "alpha" pool. 
2. We are using this hash function as part of our sharding mechanism
3. We are going to use the ketama key distribution system which is a [Consistent Hashing Mechanism](https://en.wikipedia.org/wiki/Consistent_hashing).
4. We tell Twemproxy to kick out any servers that stop responding.
5. We tell Twemproxy that we are using the redis protocol instead of memcache. 
6. We tell Twemproxy to retry the server in 2 seconds.
7. We show Twemproxy a list of servers that belong to this pool in the format `host:port:weight name`Weight is just a way to tell Twemproxy which server you'd prefer it write to. The name is a way to refer to this server consistently incase we move it about later.

With all that done, I'd recommend running the following command, which just verifies that the configuration file is valid.

nutcracker -t -c ~/conf/nutcracker.yml


Assuming it's all valid, you can just run  

nutcracker -c ~/conf/nutcracker.yml

And voila! You are now proxying your redis connections over Twemproxy. 
