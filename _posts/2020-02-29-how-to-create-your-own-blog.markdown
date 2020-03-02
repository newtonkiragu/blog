---
layout: post
title: How to create your blog using Jekyll and GitLab CI or Github Pages.
date: 2020-02-29 23:05:20 +0300
description: Well, I kinda promised, didn't I? That I would share instructions on how to create and deploy your blog using `gitlab`?
img: how_to_create_your_own_blog/header1.jpg # coming soon
tags: [Programming, Jekyll, Ruby]
category: [Programming]
author: # Add name author (optional)
---
Well, I kinda promised, didn't I? Right 👉 [here](https://newtonkaranu.me/blog/time-to-think/), that I would share instructions on how to create and deploy your [Jekyll](https://jekyllrb.com) blog using [GitLab](https://gitlab.com)? Incase you didn't know, jekyll is a static site generator built with `Ruby` while gitlab is a site used to host projects created with `git`.

### Prerequisites
There are a couple of things you need to install first before you can start using jekyll. Since I ❤️ the terminal, most of the links to the prerequisites and my instructions will be terminal based.
1. [Ruby](https://www.ruby-lang.org/en/documentation/installation/)
2. [Git](https://git-scm.com/book/en/v2/Getting-Started-Installing-Git)
3. [Jekyll](https://jekyllrb.com/docs/installation/)
4. [Npm (npm is installed with NodeJS)](https://nodejs.org/en/download/)

### Getting Started

You can get started with GitLab Pages using Jekyll easily by either forking this repository or by uploading a new/existing Jekyll project.

Remember you need to wait for your site to build before you will be able to see your changes.  You can track the build on the **Pipelines** tab.

#### Start by forking this repository

1. Fork [this](https://gitlab.com/newtonkiragu/newtonkiragu.gitlab.io/) repository.
1. **IMPORTANT:** Remove the fork relationship.
Go to **Settings (⚙)** > **Edit Project** and click the **"Remove fork relationship"** button.
1. Enable Shared Runners.
Go to **Settings (⚙)** > **Pipelines** and click the **"Enable shared Runners"** button.
1. Rename the repository to match the name you want for your site.
1. Edit your website through GitLab or clone the repository and push your changes.

#### Start from a local Jekyll project

1. Use `jekyll new` to create a new Jekyll Project.

{% highlight shell %}
jekyll new gitlabusername.gitlab.io
{%  endhighlight %}
1. Add [this `.gitlab-ci.yml`](https://gitlab.com/newtonkiragu/newtonkiragu.gitlab.io/-/blob/master/.gitlab-ci.yml) to the root of your project.
1. Setup your [theme](https://jekyllrb.com/docs/themes/).
1. Push your repository and changes to GitLab.

## GitLab CI

This project's static Pages are built by [GitLab CI](https://docs.gitlab.com/ee/ci/), following the steps
defined in `.gitlab-ci.yml`:

{% highlight yml %}

image: ruby:2.3

variables:
  JEKYLL_ENV: production

pages:
  script:
  - bundle install
  - bundle exec jekyll build -d public
  artifacts:
    paths:
    - public
  only:
  - master
{% endhighlight %}

## Using Jekyll locally

To work locally with this project, you'll have to follow the steps below:

 - Clone the repository and go into the project folder
 
{% highlight shell %}
git clone https://gitlab.com/newtonkiragu/newtonkiragu.github.io.git && cd newtoniragu.gitlab.io
{% endhighlight %}

 - Install the necessary dependencies (`gems` and `npm packages`).
 
{% highlight shell %}
bundle install && npm install
{% endhighlight %}

 - Run the local server
  
{% highlight shell %}
bundle exec jekyll serve --drafts #it will also show you the draft blogs
{% endhighlight %}


The above commands should be executed from the root directory of this project.

Read more at Jekyll's [documentation][https://jekyllrb.com/docs/].

## GitLab User or Group Pages

To use this project as your user/group website, you will need one additional
step: just rename your project to `namespace.gitlab.io`, where `namespace` is
your `username` or `groupname`. This can be done by navigating to your
project's **Settings**.

## GitHub User

To use [this project](https://github.com/newtonkiragu/blog) as your own website, you will need to rename it to a 
different name and remove the fork relationship (I prefer creating a new 
repo then setting it as an upstream to the original repo until I ensure 
things are working smoothly then delete the fork).

There is a gem (a jekyll plugin) that is used to automatically deploy the 
project to github pages. `gem "github-pages"`. All you need to do is push your work.

## Did you fork this project?
If you forked this project for your own use, please go to your project's
**Settings** and remove the forking relationship, which won't be necessary
unless you want to contribute back to the upstream project.
