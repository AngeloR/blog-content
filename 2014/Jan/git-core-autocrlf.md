# Git core.autocrlf
Linux is my development environment of choice. It wasn't always - I used to do all of my work with XAMPP and Windows, but eventually I got sick of waiting for cool things and just made the jump. Now I can't imagine actually getting any work done NOT in a terminal. 

[Vagrant](http://www.vagrantup.com/) and [Virtual Box](http://virtualbox.org) allowed me to have my linux environment for work and my Windows one for gaming. However, it means I get to run into a few issues I never have before - namely constant End-of-Line issues with git.

Windows uses the CRLF (Carriage return/Line Feed, `/r/n`) ending for lines, whereas unix uses just the LF (Line Feed, `/n`). This generally means that there's a whole mess of `^M` characters in vim due to some files having the dos ending and some being unix-y. Git will try and correct this automatically but for the longest time I had no idea how to actually set that up.

## core.autocrlf
Git has a configuration setting called core.autocrlf that tells git how you want it to handle line endings. There are three options:

- true
- false 
- input

### true
Essentially turns on autocrlf which means that if you check something in/out it will preserve the line endings that the system expects. IE: On Windows it will have CRLF endings, on unix it'll have LF.

### false
Turns it off (obviously). This essentailly leaves you alone.

### input
Converts everything to unix-y endings.

In the end I settled on `git config core.autocrlf true` for my case. It modifies the line endings for dos based files to unix-y and then leaves me alone. Exactly the kind of option I'm looking for.
