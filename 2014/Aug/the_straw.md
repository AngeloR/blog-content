# The straw that broke the camels back
Last year, I had a little mini rant about [how programmers today are missing vital knowledge (reposted this year)](http://xangelo.ca/2014/03/06/anachronistic-programming/). I wanted to flesh out my thoughts a little more and focus on a space that I think represents this problem the best: Web Developers.

## User Optional
A lot of people gravitate towards web development because it's viewed as "easier". And generally, when you look at the points that most people are comparing, they're right. 

- Getting started on web development just requires a text  editor and a browser.
- You can reload a page and see your code changes instantly
- You can live edit code until it does what you want

Man, just looking at those points makes it pretty easy to see why web development attracts so many. It's quick gratification when you're starting out, and we love self gratification. 

> Lets start by contrasting the two environments by language: Web and NotWeb.

#### Hello world in PHP, on Windows

1. Install wamp
2. Open notepad and type in `<?='Hello, World!'?>`
3. Save it as hello.php in C:/wamp/htdocs/
4. Open http://localhost/hello.php in your browser.
'
From then on, you simply edit hello.php and reload the browser page - BAM. Instant updates.

Contrast this with something a little more involved:

#### Hello world in C++, on Linux

1. Install g++
2. Open an editor and type in
``// 'Hello World!' program 
    include <iostream>
int main()
{
    std::cout << "Hello World!" << std::endl;
    return 0;
}
``
3. Compile with `g++ hello.cc -o hello`
4. Run with `./hello'

From then on after you make changes, repeat step 3 and 4.

*Note, I didn't do this in C# on Windows because really.. the steps to GET to the point where you can start coding involve at least one wizard and Visual Studio.*

You can already see that the second method is a lot more involved. Infact, as you progress and start adding more pieces to your project, building a C++ project adds more and more steps. Makefiles and header files become a must.

However, this served to separate programmers into two groups: Those who did `(user<->)code<->hardware` work, and those who did `code<->user` work. 

Now, don't get me wrong - Anyone who has code that needs to interact with a user is pretty awesome in my book. I'm not a fan of users myself. But I digress. Those people need to do a lot of extra work. Cross platform UI issues, Cross platform code, Making sure that everything looks good all the time. 

I mean, when you control a users initial response to their interaction with your project, you've got a pretty big responsibilty. 

The thing is, it's very different from a user who has to deal with a computer. And thankfully, most times these are two very different programmers.

## The last straw
Except now. Now these are the same guys, thanks to a beautiful little framework that's taking the world by storm: Node.js

See Node.js takes all of the stuff that traditional "web developers" (php, ruby+rails, asp.net) don't really care about.. and then expose it to them in a very non-threatening, accessible language. 

The nice thing is, that it lets you do some pretty powerful stuff.

The downside is, that it lets you do some pretty powerful stuff. And you know what they say about power and responsibility.

Instead of relying on a well tested server infrastructure (apache, iis, nginx, etc.), the first thing a new-comer to nodejs builds is a webserver. Or rather, an interface TO a webserver. The main power of Node.js is that it abstracts a lot of things like the actual inner workings of a HTTP request, to the point where running `require('http').createServer()` fools people into believing that's all there is to a webserver.

Without a proper understanding of what a webserver is, and how it works, it gives people a sense that they're ready for more than they are.

Thankfully, the last few years have seen a major push from developers to learn more and more about how infrastructure wokrs. the DevOps movement has brought programmers and hardware people together in a way that only really existed before hardware and software people made their divide. Couple that with the idea of a "full stack engineer" and you see software people bridging their knowledge of hardware and vice versa. 

Now I understand that as a software person you'll never fully understand how the TCP/IP stack works. And as a hardware person you'll forever wonder how `flexbox` works. The thing is, that's not important. No one is expecting you to perfect both sides of the coin.. just to realize that there's another side you need to know something about.
