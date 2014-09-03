# Making vim your IDE
I freaking love vim. Every so often I spend a couple weeks checking out another IDE to make sure I'm not missing anything and then I inevitably end up back at vim. Over time I've assembled a few plugins and workflow that make vim perfect for me.

### pathogen
[Pathogen](https://github.com/tpope/vim-pathogen) is a plugin manager for vim that utilizes git to keep plugins organized. Once you add pathogen to your vim install, you can easily add new plugins simply by cloning the repo. There isn't much to say about pathogen except that it is the greatest. 


### NERDTree + NERDTreeTabs
The first ime you pop open vim you'll notice that you can't really browse around files. You need to know the filename that you're attempting to open, as well as the directory structure. While you can get around this with some tmux file listing, it would be a heck of a lot easier if it just had a file listing like a normal IDE. [NERDTree](https://github.com/scrooloose/nerdtree) does just that - a list of directories and files that you can navigate through with your keyboard. 

[NERDTreeTabs](https://github.com/jistr/vim-nerdtree-tabs) is an addon for NERDTree that allows you to have the same NERDTree instance open across multiple vim tabs. 

### tagbar
[Tagbar](http://majutsushi.github.io/tagbar/) is something that I don't actually use that often - however it's one that I'm always glad is around when I need it. It gives you the code strucutre of a file. Classes, methods and variables are all listed allowing you to easily jump to definitions and get an overview for what content is in a file. 

Normally when I open a file I haven't been to in a while I'll pop open the tagbar and quickly glance at the methods to re-acquaint myself with things before I close it and get back to work. You can also jump straight to definitions by navigating around the tagbar, but I rarely end up doing that. There is a weird issue with having multiple buffers open simultaneously (I use a lot of vertical splits with vim) where you can't navigate to the tagbar as it displays the tags of the last split that you were in. Therefore I can't really navigate over to the tagbar from a split that isn't directly next to it. Technically I could move the splits around, but I feel like that's more trouble than it's worth.
### ctrlp
Apart from NERDTree, [ctrlp](https://github.com/kien/ctrlp.vim) is the other way that I navigate files in vim. Often times I know the file that I want to work on.. but it's buried within a huge directory structure that I don't really feel like navigating or typing out. Instead ctrlp performs a fuzzy search over the current directory and allows me to open the file within a few keystrokes.
### tmux
My development environment has always been linux - namely virtual box/vagrant which I SSH in to. This means I get a straight terminal view with minimal colors and no real "windows". In order to do a bunch of things at once, I use tmux which is a terminal multiplexer. Essentailly it allows me to replicate having multiple terminal tabs/windows within the same session. It even has the added benefit that if I get disconnected from the server I can reconnect and just re-attach my previous session. While tmux isn't actually a plugin for vim, I find using vim with tmux is a great deal better than just vim alone. I get to have a tmux window for code, for git, for mysql and for logs. 

**Install tmux**: `sudo apt-get install tmux`

### dotfiles
Now that I've kinda got my development environment customized how I like, I want to have it with me no matter where I am. I develop on multiple vms on two different machines, as well as multiple remote machines. I'd prefer if my environment was always the same. In order to ensure that I can get up and running as soon as possible on any new machine I run the following commands:

```bash
sudo apt-get install git tmux curl
mdkir ~/personal/
cd !$
git clone http://github.com/angelor/dotfiles
cd dotfiles
./setup```                            

There aren't that many customizations in my `.tmux.conf` file and my `.vimrc` ones. Mostly it's to set up plugins and to remap some keys for tmux.

