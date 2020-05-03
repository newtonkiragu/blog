---
layout: post
title: My Journey as a Software Developer human so far (Part 1)
date: 2020-05-03 12:11:20 +03:00
description: Find out how I got to where I am as a software developer
img: my-journey-as-a-software-developer/header.jpeg
tags: [Lifestyle, Programming]
category: [Lifestyle, Programming]
---
Hello world! Or is it hello the internet? 🖖 

Nah, Hey there 👋!

I'm Newton Karanu. You probaby know that already 😅. I am a full-stack software developer. 
Over the years, I have got to learn a couple of programming languages: Python, Java, JavaScript, Go, R, HTML(Yes, it is here), CSS, PhP.
During that period in time, I have got to build a couple of projects and most importantly, meet awesome people.

This blog answers two questions, [Why am I a software developer](#why-am-i-a-software-developer). [How have I gotten to where I have](#how-have-i-gotten-to-where-i-have). 
This might give you some insight on your career journey, or generally entertain you.

Recently, I got to speak with one of my friends (let's call him Malcolm), we studied in the same highschool. Though he was a class ahead of me, I think. More on this later.
He is a dev as well and before we even begun speaking, I had stalked his github and made some contributions to his repo. His code is so clean and modular.
Plus, he tries to remove ambiguity in his work. How? Here is an example.

Consider a program that scaffolds a project for you. I contributed to one such project (scaffolds a flask app for you. 
Check it out here 👉 [Flask App Structure (using blueprints)](https://github.com/newtonkiragu/flask-structure))
When getting the name of the project, here is how I approached it.

{% highlight shell %}
...
# get the project name
read -r -p "What is your flask project name? " PROJECT_NAME

# create the directory
mkdir $PROJECT_NAME

# checkout into that directory
cd $PROJECT_NAME
...
{% endhighlight %}

Here is a better, less ambiguous way to approach it
{% highlight shell %}
...
read -r -p "What is your flask project name? " PROJECT_NAME

# check if name is empty
if [ -z "$PROJECT_NAME" ] then
  # can't run without project name
  error "Must provide project name"
  return 1
else
  # get the values
  projectname="$PROJECT_NAME"

  # check validity of project name
  if [[ "$projectname" =~ [A-Za-z0-9_-]+$ ]] then
    # create the directory
    mkdir $PROJECT_NAME

    # checkout into that directory
    cd $PROJECT_NAME
    
  else
    error "Project name '$projectname' includes illegal characters"
    return 1
  fi
fi
...
{% endhighlight %}
To quote the zen of python:
> In the face of ambiguity, refuse the temptation to guess.

Back to my story. As we spoke, I remembered how I got into coding. 

## Why am I a software developer?
Growing up, I shared a room with my elder brother. When I got to around class 5, he got a dell desktop that he would use to game and watch movies.
I was not allowed to touch it at that point, only look at it from a distance. There is where I watched my first horror movie. 

Soon, he started opening up the desktop to view it's internals. I was so excited. I could hear and learn the names of the components.
Here's a motherboard. That's a ram. Cause I wasn't allowed to touch it, of course I meddled with it. I would wait until he has left the house,
then open it up and play doctor with his computer. I think I still have the harddisk bracket somewhere in a drawer. 
It was so much fun, having this forbidden fruit (How I wish the dell was an apple computer 😅).

There is where it all begun games and movies. Fast forward to highschool. I chose computer studies. 
One of my classmates (let's call him Wendo) introduced me to working in the chapel. The upside being that on weekends, we could borrow the chaplain's laptop and use it to create presentations that would be used on Sunday during the service.
Wendo introduced me to Malcolm, who would show us how to make the slides for the service. At first, we used easy worship. But that was a cracked software, so we resorted to using MS Powerpoint, another cracked software.
After creating the slides for the service, we would sit down and watch Malcolm create music using FL. I tried and failed successfully.
Wendo got the hang of that though. Soon, Malcolm started working on an awesome project that I couldn't even begin to wrap my mind on.

TicTacToe.😱 On Powerpoint.😱 Using Visual Basic.😱 I was mind blown. He was able to create a version where you could play against your friends and was working on playing against the computer before he graduated.

Continue reading part 2 👉 [My Journey as a Software Developer human so far (Part 2)](https://newtonkaranu.me/blog/my-journey-as-a-software-developer-part2)
