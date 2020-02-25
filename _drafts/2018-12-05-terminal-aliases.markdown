---
layout: post
title: Terminal Aliases
date: 2018-12-05 08:57:20 +0300
description: It gets to a point in your life where you get a paradigm shift. Suddenly, this new perspective pops into your mind.
img: # Add image post (optional)
tags: [Blog, Programming, Lifestyle]
author: # Add name author (optional)
---
The one thing programmers like is efficiency. How lean is their code, how much time does it take for their code to run? Were they fast enough? Is there a simpler way to implement it without corrupting data. A lot flows into our mind as we continue churning out applications day in day out in terms of how to scale it and make it more efficient.

What I found I was not efficient at, a while back that is, is typing. I would spend more time typing out git commands than I would spend trying to code. This became bizarre as I learnt how to explore and exploit the terminal.

I am a Linux fanatic, always switching from one distribution to another. From one desktop environment to another. One day, you will find me with mate, only to find me with Gnome soon after. From forensics and cybersecurity (parrot and kali) to generally beautiful systems (Deepin and elementary), you name it. While switching from one system to another, I am constantly tweaking it and modifying it, and trying to type my commands as efficiently as possible.

Soon I found it hectic to keep track of my aliases. These are simply shortcuts to commands I use ever so frequently. A classic example would be updating and upgrading my system every time I install a new Linux OS. sudo apt-get update && sudo apt-get -y upgrade && sudo apt-get install -f && sudo apt-get -y dist-upgrade && sudo apt-get -y autoclean && sudo apt-get -y autoremove. Whew, that was long.

Imagine having to type that every single time you install a new system. Then thereafter, bi-weekly as you try to stay with the latest software. I soon shortened the entire command with a beautiful alias, ua. (update all). I know, I know, we programmers have a tough time naming things, but more to that later on.

After doing thorough research (stack overflow and the likes), I found that I could create a GitHub gist holding all my terminal aliases. All I needed to do once I switch to a new system was to clone the gist and extract it where necessary ( in the root of the system.) Being the lazy couch potato that I am, I soon felt that typing three to four commands to setup my aliases was a little too hectic for me.

I went into a stack overflow rabbit hole trying to understand how the terminal works, and what the hell are shell scripts. Guess how surprised I was to find out that some of the commands we use day in day out, like ls, are actually aliases.

My aliases application was born. Click here to check it out.

Turns out you can create your own alias to run almost any other command in your terminal.

To create a new alias, simply open .bashrc or .zshrc if you are on Linux, and .bash_profile if you are on a mac in your favourite text editor and write your alias in the following syntax

alias name-of alias='command to be run' for example,

alias st='git status'
You can make the alias a function too

# create and go into a new folder
mcd() {
  mkdir $1
  cd $1
}
Soon thereafter, I came up with an understanding that shell scripts are code written in shell and will be run in the terminal. Whole topic coming soon.
