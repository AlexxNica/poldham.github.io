---
layout: post
title: "Creating a website on Github using Rmarkdown with Jekyll and servr"
published: true
---

I am pretty new to using R and to Github, but I liked the idea of creating a static website on Github and then publishing Rmarkdown both to my project repository (on patent analytics) and to a static website. What I didn't want to bother with, amid learning R, was messing around with Wordpress, Content Management Systems, hosting packages and complicated templates. 

Having never heard of [Jekyll](http://jekyllrb.com/) I found it a bit intimidating at first but cheered up when I read Tom Preston-Werner's [Blogging Like A Hacker](http://tom.preston-werner.com/2008/11/17/blogging-like-a-hacker.html) article on the background to Jekyll. This made sense to me and so I decided to brace myself and go for it. 

There are a few ways to get started and they all work. I'll start with the way I found worked for me and then the other ways. Bear in mind that you may prefer the other ways. 

##My preferred route.

Assuming you already have a [GitHub account](https://github.com/) (it takes no time at all), I found that the easiest way to get started is to follow Barry Clark's excellent guide to [Jekyll Now](http://www.barryclark.co/introducing-jekyll-now/) for creating a user site. There are two flavours of GitHub pages sites, users and projects. I started with the user site because it is easier. This involves forking the [Jekyll Now GitHub repository](https://github.com/barryclark/jekyll-now), replacing the name with your own, following some simple instructions and you have a functioning site in a few minutes. 

It is easy enough to edit and create posts or new pages directly in Github. The instructions provide a link to [Prose by Development Seed](http://prose.io/) on GitHub, more info is on their [website](https://developmentseed.org/blog/2012/june/25/prose-a-content-editor-for-github/). 

A more detailed follow on guide is [here](http://www.smashingmagazine.com/2014/08/01/build-blog-jekyll-github-pages/).

I then cloned the repository to my machine and have been working through editing and adding pages by copying and using TextWrangler on the Mac. The next task is to convert Rmarkdown to Github flavoured markdown (more on this below) and I will be done. 

##Other ways to get started

Here are the other ways I tried. 

1. You can simply go to [Jekyll](http://jekyllrb.com/) and follow the v. fast instructions leading to the [GitHub Pages instructions](https://pages.github.com/). It worked as it said on the packet but I felt I needed my hand holding a bit more. 
2. [Jekyllbootstrap](http://jekyllbootstrap.com/) also offered a quick start and worked. I guess what I was less happy about was that I had no idea what was really going on. You may be different of course.
3. I also tried the GitHub help [Using Jekyll with Pages](https://help.github.com/articles/using-jekyll-with-pages/). I'm running Mac OSX Yosemite and found that I struggled with the [gem install bundler](https://help.github.com/articles/using-jekyll-with-pages/) step. I found the [RailsApps Project](http://railsapps.github.io/installrubyonrails-mac.html) article really helpful in getting the machine organised before heading back to the instructions. 

##From Rmarkdown to Jekyll

Yihui Xie and others at [RStudio](http://www.rstudio.com/) have developed the servr package as a simple HTTP Server to Serve Static Files or Dynamic Documents. The beauty of this for our purposes is that it can be used to preview documents in a browser in RStudio and publish Rmarkdown documents direct to the Jekyll site on GitHub. 


{% highlight r %}
install.packages("servr")
{% endhighlight %}

{% highlight r %}
library(servr)
library(knitr)
{% endhighlight %}



##Other Guides and Resources

1. The [Jekyll Documentation](http://jekyllrb.com/docs/home/) is helpul. 
2. Adam-p's [Markdown Cheatsheet](https://github.com/adam-p/markdown-here/wiki/Markdown-Cheatsheet) on GitHub is really handy.
3.
4. [Made Mistakes](https://mademistakes.com/) is a cool Jekyll website by designer Michael Rose. 
4. For R User Yihui Xie at RStudio has developed [servr](http://yihui.name/knitr-jekyll/2014/09/jekyll-with-knitr.html) that with knitr will directly serve R pages to Jekyll for websites.
5. For R Users [Jason Bryer's article and code](http://jason.bryer.org/posts/2012-12-10/Markdown_Jekyll_R_for_Blogging.html) provides a solution to using RMarkdown with Jekyll for GitHub pages
6. Jerid Francom has a nice article discussing [publishing Rmarkdown to Wordpress and Jekyll](http://francojc.github.io/publishing-rmarkdown-to-wordpress-or-jekyll/)
