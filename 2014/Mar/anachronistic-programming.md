# Anachronistic Programming
> I've decided to repost this article that I originally posted on September 17, 2013 while cleaning up the blog archives from when I was using Fargo. 

I want to show you a piece of code. Something that's touted whenever this language is spoken of, and everyone seems to be able to pull out of their ass. I want you to look at it, understand it and then see how far down the execution chain you can take it. I'm not talking about if you can debug the app, set a breakpoint and then step through it. I want you to sit there, hands off the keyboard and go through the request cycle that needs to occur for this particular piece of code to execute and run as you expect it to. Spare no detail.

<script data-gist="gist6605487" src="https://gist.github.com/AngeloR/6605487.js"></script>

Did you get far enough? Did you get down to the HTTP protocol? The packet dance that happens before the actual request from a browser is sent? Or did you stop at "Browser makes a request to the IP address"? 

See the problem today isn't that the computer is this magic box that only a few can understand. It isn't relegated to the guys in beards and thick glasses. It isn't just for the geeks and nerds. To be a programmer meant that you needed to also understand the specific hardware stack that you were working on. The exact chipset, the exact instructions available to you. The exact specs on the memory and video controllers.

Today, computers have become common place. And in order for it to get to this stage a few things needed to happen. The first one being "It just works". That's the basis of the consumer computer. With no fiddling, no worrying about any kind of internals, you should be able to get up and running in no time. 

But you're not just a typical consumer. You're a programmer. And unfortunately, this idea of "It just works" has found its way into programmers minds everywhere. You don't need to think about the HTTP protocol, "It just works". You don't need to worry about Little vs Big Endian - "It just works". 

*Until it doesn't.*

I think the problem with programmers today is quite simple. We've been lead to believe that we can rely on certain things within the system. Which, is great. I mean, if we couldn't rely on the HTTP protocol where would we be today? But this reliance has led to an entirely new problem - _"I don't care"_. Programmers today don't need to learn about how the protocol works because "It just works". They don't need to think about it. And I think that has lead to an entire generation of programmers who don't understand the fundamentals of programming. They don't understand that the code they type into their fancy IDE's is really powered by the ideas of a few people and run on hardware. There's a severe disconnect between hardware and software and that is hindering them without knowing it. 

Don't get me wrong, I'm not trying to say that I'm some incredible programmer - far from it. I'm actually a terrible programmer, because programming isn't all software and algorithms. There's a hardware component to it that's overlooked way too often. The things you're doing with code you're RELYING on the hardware to accomplish. 

Don't you think you should at least have a vague understanding of how it works?
