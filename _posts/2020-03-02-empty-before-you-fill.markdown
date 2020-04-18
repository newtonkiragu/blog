---
layout: post
title: Empty Before You Fill.
date: 2020-03-02 08:15:20 +0300
description: Just read everything as if I’m smiling and I have a mischievous little twinkle in my eye.
img: empty_before_you_fill/header.jpeg # coming soon
tags: [Programming, Python]
category: [Programming]
---
> You will have a hard time learning from someone with more knowledge if you already know everything.

It was a nice Morning, you know, the one that you wake up psyched up. Those days when you wake up before your alarm goes off. It was one of those days when I read that specific quote in a book that I had been putting off to read for quite a long time. But as I said previously,
`I have time` and I intend to use it skillfully and artfully.

### Learn Python the hard way
I already know some bit of programming, like a tiny drop in a vast ocean 😅. I always feel like a fraud because there is so much more that I need to learn, and not so much time and space to learn it. 
So I picked up a book called learn python the hard way, deciding to have `shoshin`, the beginner's mindset as I go through the book and practice and learn.

My plan is simple, having only four steps to it.

1. Write exercises using my text editor, `vim`.
2. Run the exercises I wrote.
3. Fix them when they are broken.
4. Repeat.

### Warnings, reminders, more warnings and Errors
From the very word go, there are so many warnings and disclaimers. On the first exercise, I am given a reminder that I should have my environment set up already. Furthermore I am warned not to go on if I have skipped that step as I will not have a good time, then warned and reminded that that is the last time they will start an exercise with a warning not to get ahead of myself.

Sidenote from the editor:
> I might make a series out of this depending on the next few exercises. I will use [pynotes](https://github.com/newtonkiragu/pynotes) to log things I learn. Right, moving on swiftly.

The beauty of learning python the hard way is I have to literally learn it the hard way. The book uses `python2.x` while currently the world is at `python3.x`. The first time I learnt python, it was using python3, so what is happening is I am going to give myself hell because i have to 
1. Type the exercise as is in python2

{% highlight python %}
# example1.py (python2)
print "Hello World!"
print "Hello Again"
print "I like typing this." #lol
print "This is fun."
print 'Yay! Printing.' #see what I did there? Pay attention!
print "I'd much rather you 'not'."
print 'I "said" do not touch this.'
{% endhighlight %}

2. Loop through the 4 steps mentioned above 👆.
3. Convert the code written to python3.

{% highlight python %}
# example1.py (python3)
print("Hello World!")
print("Hello Again")
print("I like typing this.") #lol
print("This is fun.")
print('Yay! Printing.') #see what I did there? Pay attention!
print("I'd much rather you 'not'.")
print('I "said" do not touch this.')
{% endhighlight %}

4. Repeat step 2.
5. Convert the code written to python3 with backward compatibility (_is this even a real thing?_).

{% highlight python %}
# example1.py (python3 with backword compatibility i.e can be run with python2 as well)
from __future__ import print_function

print("Hello World!")
print("Hello Again")
print("I like typing this.") #lol
print("This is fun.")
print('Yay! Printing.') #see what I did there? Pay attention!
print("I'd much rather you 'not'.")
print('I "said" do not touch this.')
{% endhighlight %}

6. Repeat step 2.

The end result would be a really strung up programmer, possibly with a lot of rage 😤 to go around but who might have fun and learn so much🤪.
> What is living if you cannot take risks and plough through discomfort.
