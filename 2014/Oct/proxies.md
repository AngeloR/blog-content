# Proxies 101
At it's core, a proxy is a service that is designed to act as a "middle man". 
That is, if there are two parties (Website, You) that are trying to communicate 
neither of you talk to each other directly. Instead, you talk to a "proxy", 
which then relays your information to the website. In return, the website 
talks to the proxy, which then relays the information back to you.

<div align="center">
    <img src="http://i.imgur.com/9jCQUui.png" alt="Understanding Proxies" />
</div>

A basic conversion between YOU and MY WEBSITE if you connect through a proxy 
might look something like this.

1. You tell the proxy: "connect to http://xangelo.ca"
2. The proxy connects to http://xangelo.ca and requests the home page
3. I give the proxy the home page
4. The proxy gives you the home page.

Pretty simple right?

Of course, the implications of this are enormous! I'll touch on this more later 
on as there are a LOT of benefits of running behind a proxy.

Of course, not all proxies are made equal, and there are many different reasons 
to use one.

## Types of proxies
Proxies can be broken down depending on what layer of the [OSI model](https://en.wikipedia.org/wiki/OSI_model) 
they function on. Each has its benefits and drawbacks, and depending on what 
you are using a proxy for, one might be better than the other.

### Layer 4 Proxies
If you're not familiar with Layer 4 of the OSI model, it's the "Transport" 
layer. At this layer, the proxy doesn't see a "URL", but instead it sees IP 
addresses. 

Proxies are faster if they function at this stage, because as soon as they know 
the IP address of what you're trying to get to, they can forward the traffic 
there.

### Layer 7 Proxies
This layer is the "Application" layer. At this layer, the proxy can see the 
specific URL you are trying to access and even the content that is flowing 
back and forth.

### Forward and Reverse Proxies
In addition, you may hear about "Reverse" and "Forward" proxies. The thing is, 
apart from a bit of technical jargon, these proxies function almost exactly 
the same way. A forward proxy "forwards" your requests to the internet. A 
"reverse" proxy forwards requests FROM the internet to a series of recipients.

Generally forward proxies have a single user that is making the request, whereas 
a reverse proxy has multiple recipients that will handle the request from the 
internet.

## The benefits of a proxy

### Personal Anonymity
By placing a proxy between you and a website, the website won't know that 
YOU are accessing it. It will think the proxy is. A common use for this scenario 
is to have a proxy in one country that you access. Any websites you visit 
through the proxy will think you are coming from Country A, when you actually 
reside in Country B. 

This idea is the basis of technologies like TOR. Instead of connecting directly 
to a website, you connect through what is essentially a series of proxies 
and the website you are attempting to connect to will only see the details of 
the LAST proxy. Of course, your traffic is still traceable through the proxy 
chain, but every hop makes it a LOT harder.

### Load Balancing
Load balancing is exactly what it sounds like. Imagine you're given a 300 pound 
barbell. Instead of holding it in one hand, you use both your hands. This way, 
you're not putting unnecessary stress on one hand - you're balancing the load 
across both hands.

When it comes to web services, we "Load balance" to direct traffic between 
multiple servers so that one server is trying to handle everything. This allows 
us to have smaller servers, but also to have redundancy. If one server is not 
functional, we can still serve our users because we have another one.

If you have a fairly simple web app (The entirety can be on a single server), 
you can have multiple servers behind a proxy, you can use a Layer 4 Reverse 
Proxy to balance traffic between them.

If you have a complicated web application, you can have a single URL, and then 
using a Layer 7 Reverse Proxy you can route the user to different components 
of your application. If a "Service Oriented Architecture" system, a Layer 7 
Reverse Proxy is pretty essential.

### Security
Today, everyone runs an anti-virus to protect themselves from malware and 
viruses. However, when you run a company, buying anti-virus and managing it for 
hundreds of users is a LOT of cost. It would be better if you could do it all 
in once place.

By routing all requests through our proxy server, we can can the content that 
websites send back and run it through virus detection software we can ensure 
that all employees aren't getting viruses and malware sent back to them.

Proxies are, in addition, what power the black/white listing functionalities 
that you find at various companies. With a blacklist, you can enter a URL or 
IP address (Layer 7 or 4 respectively) and users that attempt to access those 
websites are given stopped.

### Data Leakage Prevention
In addition to stopping malware and viruses from getting in to a company, a 
proxy can stop data from leaving a company as well. In large corporations, 
data theft is a big issue and being able to detect data loss. By passing 
data leaving the company through a DLP solution (part of which includes a 
proxy) it allows you to stop data leakage before it happens.
