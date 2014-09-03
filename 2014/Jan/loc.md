# Lines of Code
Lately there's been talk again about "Lines of Code" as a metric for progress on a project. The idea is, developers are being graded based on how many lines of code are checked in on a daily/weekly timeline. Unfortunately, not only is this unbelievably stupid, it's also not "new" stupid. It's the kind of stupid that's just been around for a while. 

> In early 1982, the Lisa software team was trying to buckle down for the big push to ship the software within the next six months. Some of the managers decided that it would be a good idea to track the progress of each individual engineer in terms of the amount of code that they wrote from week to week. They devised a form that each engineer was required to submit every Friday, which included a field for the number of lines of code that were written that week.
> Bill Atkinson, the author of Quickdraw and the main user interface designer, who was by far the most important Lisa implementor, thought that lines of code was a silly measure of software productivity. He thought his goal was to write as small and fast a program as possible, and that the lines of code metric only encouraged writing sloppy, bloated, broken code.
> He recently was working on optimizing Quickdraw's region calculation machinery, and had completely rewritten the region engine using a simpler, more general algorithm which, after some tweaking, made region operations almost six times faster. As a by-product, the rewrite also saved around 2,000 lines of code.
> He was just putting the finishing touches on the optimization when it was time to fill out the management form for the first time. When he got to the lines of code part, he thought about it for a second, and then wrote in the number: -2000.
> I'm not sure how the managers reacted to that, but I do know that after a couple more weeks, they stopped asking Bill to fill out the form, and he gladly complied.
- via <cite>[Folklore.org](http://www.folklore.org/StoryView.py?project=Macintosh&story=Negative_2000_Lines_Of_Code.txt&sortOrder=Sort+by+Date&topic=Management)</cite>. 

Interestingly enough, this silly idea is back yet again. A recent post over on [/r/programming](http://reddit.com/r/programming) talks about a [teacher who grades based on LoC](http://www.reddit.com/r/programming/comments/1vtezz/a_friend_wrote_this_code_for_a_class_where_were/).

## Senior developers write less code
Here's the thing. I believe that the newer you are to programming the more time you spend programming. Think about your early projects - you had an idea and you just jumped right into it didn't you? You knew exactly what you wanted to do, exactly what features you wanted, and you just hacked at it until it was done. You hit that [Builders High](http://randsinrepose.com/archives/the-builders-high/). When you're new to programming you chase that high as ferverently as possible. You've never tasted anything quite so sweet. 

Unfortunately, the time eventually comes to make some updates to your software. And you think "You know what, if I just re-write it with what I know now.. it'll be like 10x better!". And off you set yet again, chasing that high. The thing is, eventually you get sick of building the same thing over and over again and you eventually decide to just build it smart the first time. 

So you sit down and plan out the requirements, you organize the database, and you organize your folder structure. You set up npm, Grunt and LESS. And before you know it, your done your day without a single line of code being written. But you feel productive - because you're no longer a code-monkey hacking out LoC. 

## Not a builder, an architect
See the difference between a Jr. dev and a Sr. dev is simple. Forethought. It's the act of sitting down and actually figuring out the best way to do something. To plan and research methods before deciding on what's best for the situation. You're no longer just building software. Now you're architecting a solution. You have to see the vision at the end, and then imagine all the little pieces and how they'll work together. As a Sr. developer you won't spend as much time writing code as you will planning code. You'll spend a heck of a lot of time planning. And you'll love it because you know it's the right way to do it. 

Just the other day I was speaking to another developer about some new features they were planning on adding to their site. Turns out the software was designed with the eventuality of adding these features. Actually implementing them required a handful of changes and some testing time as opposed to the weeks it was originally estimated that it would take to augment the current application with the new features from scratch. 

That's what the Sr. Developers best asset is. Forethought. 

See you're not paying a Sr. Developer for how many lines of code they're writing. You're paying them for all the lines of code that no one needs to write.
