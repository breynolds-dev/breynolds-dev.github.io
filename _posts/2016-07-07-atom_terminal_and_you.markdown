---
layout: post
title:  "Atom, Terminal and you"
date:   2016-07-07 16:35:18 -0400
---


Recent discussions with a few people got me thinking about productivity and personal preference. When I first started working to learn programming I was using the default OS X terminal, basic Atom settings and my own ignorance of the way things should be. Now after hours of tweaking and searching online I have started to see how much more efficient my work can be. All it took was someone to show me where to start and a little bit of work to get it setup the way I wanted.

So here I am hoping that I can show even just one person where to start and get their mind working on what they can do next


**Terminal**

The OS X terminal in my opinion will be the second or third most important thing you’ll use to program (if you’re on a Mac). I never really thought about how to customize it or even if I should. For me a terminal and bash prompt has always just been whatever I was given and I used it to the best of my ability. Diving into it deeper now I realize that I can do so much more with it. Simple little changes like adding a clock and my git branch started to make life so much easier when moving around and cloning, adding and committing things. I took that and then decided I could take it even further and thus I ended up with something like this.

![http://i.imgur.com/89FzfSu.png](http://i.imgur.com/VrWboJo.png)

I know it doesn’t seem like much, but for me it’s perfect. I have a nice clean interface for my terminal prompt where I can quickly see the time, the entire directory structure of my current folder and even a nice highlight to show what my current folder is. Then on the right we have my git branch that’s easily accessible and readable for me so I always know which branch I’m working on. I tried several different things like battery percentages and all sorts of little scripts, but most of them seemed to just detract from the nice clean look I was going for.

There are several different terminal shells you can work with like zsh and I spent some time playing around with them, but in the end I felt like bash worked best for what I wanted. I’m not sure why, it just felt better. Each person is going to be different and if you feel like one of the others works better for you then use it! Don’t get stuck using something that feels clunky or that is a headache for you.


**Aliases** & **Bash Functions**

The second half of my bash experience has been using aliases and functions to automate my work for me. The less I have to type and the less I have to move my hands to use the trackpad or click around on different programs the more productive I feel. All with just a few little lines. I’m going to post a few of them here:

```
#Used to reload the bash shell after making changes
alias reload="source ~/.bash_profile"

#Open's the .bash_profile in atom editor quickly
alias bashprofile="atom ~/.bash_profile"
```

Those two quick little aliases made it easy for me to get into my bash profile for editing, and reloading my bash shell after making changes. These two aliases don’t really accomplish much, but they saved me a lot of time.

```
#Creates a Directory then CDs right into the new directory
function md { mkdir $1; cd $1; }
```

This little function is just a nice little time saver when making directories for applications, or even just something to hold files.

```
alias gs="git status"
alias ga="git add"
alias gb="git branch"
alias gcl="git clone"
alias gcm="git commit -m"
alias gco="git checkout"
alias hc="hub create"
alias gpom="git push origin master"
alias gcom="git checkout master"

function gclone {
      reponame=${1##*/}
      reponame=${reponame%.git}
      git clone "$1" "$reponame";
      cd "$reponame";
}
```

These aliases have become my life. I’ve been using github so much recently cloning lessons, making changes and pushing commits back. Changing branches and even creating new repos that if I had to keep only one set of aliases this would be it. Some of them spawned just because I wanted to be lazy and type gcm instead of git commit -m and others make life so much easier. For example the gclone function just cd’s you into the directory of the repo you’ve just cloned. How nice is that? I just gclone somerepo.git and bam I’m in the directory ready to start working. You can even take it a bit further and automate your bundle install and atom . commands into that same function so now it’s opening your editor and making sure you have all the correct gems installed.


**Atom** or **Sublime**

A good text editor has to be the most important tool for almost any programmer. While I do love a good clean terminal prompt, a text editor like Atom or Sublime can make your life SO much easier and you might not even know it!  Before I get too in-depth here I should say that I've chosen to use Atom over Sublime. Both are good options and I think they are accepted almost anywhere, however I just liked Atom better. Nothing bad about Sublime and you'll see it used in a lot of the example videos. Again it's all about personal preference and a lot of the times it comes down to which you were exposed to first.

Right out of the box these editor's give you so many nice tools due to the packages or plugins that they come with. Auto completion, auto closing tags, bracket matchers (because who hasn't spent hours finding a missing bracket), and so much more. However that's just the beginning. You can find user submitted packages out there to download that continue to make life easier. I've thrown together a list of some of my favorites.

* [auto-update-packages](https://atom.io/packages/auto-update-packages) While this plugin is simple it helps to make sure all the rest of your packages are up to date with the latest fixes and features. Sometimes a new feature will break things, however more often than not you're going to find it helpful.
* [file-icons](https://atom.io/packages/file-icons) This simple little package just helps to make filetypes easier to identify when you are browsing the file tree. Clean, simple, elegant.
* [color-picker](https://atom.io/packages/color-picker) & [pigments](https://atom.io/packages/pigments) are two great plugins if you do anything in web design. Not only does it allow you to use a nifty little color popout to pick the color you want to use, it will also change the background behind that color text to give you a visual representation of every color code in your css or html file.
* [open-in-browser](https://atom.io/packages/open-in-browser) is a nice little plugin that makes previewing your html or css changes a little easier by giving you a quick right click menu option to open whatever page you right-clicked on in a web browser. Just a quick little time saver.
* [terminal-plus](https://atom.io/packages/terminal-plus) is another one of those time saver plugin's I like that means I don't need to leave my atom window to access the terminal. It even loads my custom bash prompt, yay!
* [git-plus](https://atom.io/packages/git-plus) is the last of the plugin's that I almost cannot live without anymore. Git Plus allows me to do so much with my git repos with a few simple clicks. I can add all, commit with a message and push all the files to my active branch with one click.  With this I'm doing commits more often so that I have a better record of all of my changes.


Finding the right environment is really up to you, everything you do needs to make YOU feel happier and more productive. I have looked at the development environments other people use and I try different programs, different plugins and even different window layouts. In the end however it all comes down to what works for you. No two environments should be the same because no two people are the same. Just have fun with it!

