#Building your API - The  things everyone forgets
If you've been a developer for the last few years you'll know that everyone and their mother seems to care about APIs. I've talked to many clients who always seem to want the same thing: 

> We want an API first, then we can build the website and have mobile apps built around that.

And you know, when you think about it, that makes a lot of sense. Instead of building out a codebase multiple times you build it once as an API. Then if you planned things properly all your future projects can interact with your API to deliver the content as your users expect. And it isn't just limited to something as basic as "web" vs "mobile" versions. You can use the same API to start creating systems that aggregate stats, to create administrative views into your content and so on. APIs, thankfully, are pretty flexible things. 

However, there is a cost associated with this flexibility that a lot of developers forget about. By being this flexible you are opening yourself up to a lot of future issues. Too many developers forget the fact that they're building an API so that other users can connect to it. You need it to be fast, available, scale well, and you need it to make sense. 

### HATEOAS - Don't get bogged down
There's a lot of talk of [HATEOAS](https://en.wikipedia.org/wiki/HATEOAS). If you haven't heard much about it, consider yourself lucky. Die-hard ReST users insist that you need support for HATEOAS. The Spring framework [has support](http://projects.spring.io/spring-hateoas/) for it as well. The thing is, for all the well intentions behind HATEOAS I think it forgets something fundamental. 

> Unless you're attempting to build a system to dynamically generate API client libraries - NO ONE IS GOING TO CRAWL YOUR API

See the thing is, APIs are used for something. Someone has made the concious decision to integrate your API in an attempt to accomplish something. They have a task that they need accomplished in a particular manner - they are not going to crawl your API and figure it out themselves. 

Because of this requirement, most developers will spend some time organizing their workflow based on the *API DOCUMENTATION* that you provide. The better the docs are, the easier they are to follow, and the harder they are to create. I mean, let's be honest here - good documentation is REALLY HARD.

Infact, I have a sneaking suspicious the love of HATEOAS is mostly by people who are just trying to get away from doing an REAL documentation. I'm not talking about code docs. I'm talking about documenting use-cases to ensure that for the majority uses for your API you have some kind of walkthrough for people. Although, this may be less important if you...

### Make sure your API makes sense!
While it won't let you get away from ALL documentation, having an API that makes sense, and is easy to follow is a god-send. ReST forces the idea of "resource pointers" so if you're following proper URL defining principles, you should mostly be good to go. 

A good API might be defined as follows. It clearly defines endpoints, labels the properties that can be passed to a URL and uses standard HTTP Response Codes to inform the user of errors. 

GET     /users - Returns: 200, 400, 401, 409, 500
POST    /users - Returns: 200, 400, 401, 500
GET     /users/:user_id - Returns: 200, 400, 404, 500

In this, we clearly define our endpoints, and what attributes are expected where. We even tell the implementer what error codes they receive (these are standard HTTP response codes which have pre-defined meanings). 

However, note that we are using POST /users instead of PUT /users. ReSTful architecture defines that the PUT verb is what we should be using to actually create a resource, and then we should be POSTing information back to the resource id returned from our PUT. 

However, in the real world, we have to make a few concessions. Yes we could implement PUT, but we need to really think about what our app is doing. If we are Twitter, telling someone to make a "PUT" request to reserve a tweet_id before sticking some content in is ridiculous. But if we are Dropbox, maybe it makes sense to send a "PUT" request to create a placeholder for our content and then update the resource ID with the content at a later time. 

Having your API make sense isn't just about following the "rules" - it's about ensuring that for the majority of the users of your API, using your API is a smooth a process as possible. 

### Plan for scalability, not for scale.
This is something that gets a lot of devs. 

> Your incredible new platform is ready to hit the world and revolutionize an industry. Today you're just a nobody - tomorrow you'll be the most talked about Entrepreneur in the your industry. Once you launch everyone will flock to your API in droves. I mean, who wouldn't, right? 

A lot of devs over-engineer the API. They plan out elaborate infrastructure that they claim will handle <strike>thousands</strike> millions of users concurrently. It's going to be an engineering marvel. Of course, it's going to cost a pretty penny - what do you expect?

The problem is, realistically, tomorrow you're not going to have millions of users. You're going to have 5 because you called your mother and told her to take a look at it. You're not going to be at scale tomorrow. Or next month. If you're one of the lucky few, you'll hit something viral and in 5 or 10 months you'll start going at the pace you expect. Realistically, you'll plod along for the next couple years tweaking your product to better fit the market.

It's far better to ensure that your API can scale UP to millions of users, than for your API to handle millions of users on day one. There is a lot of infrastructure required to handle millions of users, and your API needs to be able to seamlessly move from 3 servers to 50 without anything breaking or any downtime. 

### Don't forget to version your API
At some point you are going to need to make some breaking changes to your API. If you haven't thought about some kind of versioning strategy you are in for a few headaches. 

When people get something working with your API, they'll rarely revisit it to "upgrade to your fancy new version". Heck, they'll avoid it for as long as they can. So you'll need to be able to define a new version in your API url (api.yourcoolapp.com/v1/ and api.yourcoolapp.com/v2 work rather well). But you'll also need to ensure that they can run in tandem. 

Ideally, when you release v2, v1 will go into "deprecated" mode and when v3 comes out, v1 will finally be removed. You need to ensure that your input/output remains the same within a version or you'll have some very upset implementors. 
