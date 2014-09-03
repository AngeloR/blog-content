# New Blog System
Every so often I feel the need to reinvent the wheel. Contrary to [popular 
belief](), I find that reinventing it is what keeps me fresh. It helps me apply 
new ideas and concepts to a problem I am already intimately familiar with. It's 
easy to apply a new concept to a new problem - but getting out of the rut of 
thinking a certain way takes some time.

## Problem 1: Saving my content
One of the biggest issues I had when moving between Wordpress installations, 
and even between Wordpress and Ghost was migrating posts. As a result, whenever 
I switched blogging platforms I lost some great content and ideas, which in 
turn resulted in me losing a lot of great comments to posts. I hate that this 
happened, but each time I moved I made the decision that it was just too much 
work to do. There were hundreds of posts that needed to be moved between systems 
and it was easier to just start from scratch. 

When I moved to Fargo, I initially thought that it would let me keep my content 
and presentation separate. I was wrong. Fargo took the content, displayed it one 
way, but then saved it as OPML. Sure it gave me access to the OPML, but I spent 
a couple days writing a proper parser just to get that content out. Most times, 
I couldn't. It would add too much HTML into the content.

When I moved to Ghost, I was excited because all my content would be in Markdown. 
Of course, Ghost keeps it all in a MongoDB instance, but it was trivial to get 
the plain-text out. Once I had done that, I vowed that I wouldn't deal with 
that issue again. My next blogging platform would need to work like an API. I 
would provide the content in plain-text, and request certain pieces, or lists, 
and the system would provide it to me in the manner requested. You know, proper 
ReSTful procedures.

For the new system, I've employed a completely separate git repository that 
holds the content I write. It's simply a sub-module of the final repo meaning 
that I can update the content and have it all versioned and tracked. And it 
even means that readers can submit their own fixes to any issues they find.

## Problem 2: Presentation
Since I get bored with a design pretty frequently, I wanted to ensure that my 
next site would have true design separation. Since there was a backend server 
that was providing the content, I could write my own single-page-app that would 
display the content as necessary. It allowed me to keep the presentation logic 
completely separate from the server and ensure that I could swap up the design 
whenever I felt like. 

To achieve this, I once again relied on git submodules. By creating the ui as a 
separate git project, I was able to modify it independently of the server 
allowing static caching (nginx) to handle serving up the pages. 

> By keeping things separate like this I think I've finally found a blogging 
system that I like. 
