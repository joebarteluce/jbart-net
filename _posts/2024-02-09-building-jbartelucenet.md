---
layout: post
title: Building jbarteluce.net
lead: Creating a personal website for (almost) free
---

This post is not a guide or tutorial on how to build your own website (there's plenty of those). Instead, I will discuss my own experience in this endeavor, including some of the technologies used and the thinking which drove me to use one technology over another.

# Where To Start?

In the beginning, I wanted to write everything by hand. Being a student of Computer Science, I do love me some good code, and I figured learning HTML and CSS would be a cool thing. The easy solution would be to use a Content Management System like Wordpress, or even one of those Push Button, Get Website services like Wix. Instead, I wanted to learn the languages of the web, and arrive at the end with new skills, bragging rights, and importantly, something unique. 

Spoiler Alert: This did not last long.

HTML and CSS aren't hard languages. However, I did encounter two difficulties: time and visual design. Learning a new language is a time-consuming prospect, and while I was eager to embark on this journey, I had already committed most of my waking hours to a full load at university. Progress was slow. What slowed me down even more was the visual aspect of the website. What colors should I use? What "theme" am I going for? Where should the buttons go, and the links? I can recognize when something looks good, but as it turns out, I'm not a graphic designer. I can't even pretend to be one!

Hitting a roadblock, my website sat for weeks. There was a too-large picture of me, some cards I'd made with CSS, and a strange green text clashing against a background picture of the supergiant star Betelgeuse. No good. However, I wasn't ready to throw in the towel and pay for a Wordpress site. So I went searching. 

# Discovering Jekyll

What I found was [Jekyll](https://jekyllrb.com/), a really awesome open-source static website generator. Jekyll takes source files, written in HTML and Markdown, combines them with a theme, and outputs a lovely folder filled with a complete website. What this meant was I could create my website content without worrying about the code to make it look good. Furthermore, a static website is highly performant, translating to fast load times and near-universal compatibility.

## Themes

There's a plethora of themes written by talented and generous folks who share their work for free. I was able to find one I quite liked, [cvless](https://github.com/piazzai/cvless).

## Installation

![Jekyll CLI](../assets/files/Screenshot%202024-02-12%20at%205.36.19 PM.png "Building jbarteluce.net from the CLI")

Getting Jekyll onto my Mac was a breeze. A few lines on the terminal got Jekyll and my chosen theme onto my machine. Another line generated a new website, and then editing two lines of the new website code applied the theme. Finally, the command 'jekyll build' built my website. Bam!

## Have Your Cake and Eat It, Too

With my shiny new website brought to life, things were good... for a few minutes. It didn't take long for me to decide that I wanted to change a few aspects of the theme. I didn't like some of the icons, I wanted to chop off half of the landing page, change how the blog works, etc. Fortunately, everything is open source. So I started looking around in the source files to see how things work. Before long, I was making changes to the HTML, adding new svg files for icons, and generating new pages. This is the most satisfying thing about Jekyll: you can code the interesting stuff without sweating the details of the framework. For me, this meant the best of both worlds, getting a nice-looking website, and one that I can mess around with under the hood. 

# Hosting 

> What is there more kindly than the feeling between host and guest? <br> - Aeschylus, ancient Greek tragedian

A website needs a place to live, and there are plenty of options. For a personal website that won't get much traffic, a really good free choice is [Github Pages](https://pages.github.com/). You can host your site with a free subdomain, for example joe.github.io. It's also dead simple to use, because your website is stored in a repo, enabling you to use any "Git-fu" you may have already learned. In fact, I already had a website hosted there, a little html number that I spun up for fun. 

Instead, I chose a different route. This semester, I'm learning Amazon Web Services (AWS). Perhaps the King of the Cloud, AWS offers over 200 products, including web hosting. Hosting my humble site on AWS is major overkill, but it has been a nice opportunity to apply what I'm studying in class. And, they offer free-tier! Free is my favorite cost.

## S3 Buckets and Route 53

After creating an account, the first step is setting up an S3 bucket. I enabled public access and static web hosting on the bucket, and uploaded my website files. The service provided an endpoint URL, and my site was live instantly. But http://jbarteluce.net.s3-website-us-west-2.amazonaws.com/ is kind of a mouthful, so I opted to part with a few bucks ($12 to be exact) and registered my top level domain [jbarteluce.net](https://jbarteluce.net). This was pretty easy with Route 53, another AWS product. The domain propogated out to DNS servers within minutes. 
 
## CloudFront and Certificate Manager

Things were going well, except for the absence of the padlock in my browser when my webite was loaded. S3 buckets can't serve files with https. To fix that, I used yet another AWS product, CloudFront. This is a CDN service which can serve files using TLS, and as an added benefit, serves the website super-quick. I set CloudFront to cache my S3 bucket with a few clicks. As of this writing, my website may well be in geographic locations across the US. If anybody were to access it, it would be a low-latency high-bandwidth affair! 

There was only one thing left to do. The SSL certificate was the final key to the padlock puzzle. Using Amazon's Certificate Manager, I applied for an SSL cert on [jbarteluce.net](https://jbarteluce.net) (free dollars). It was granted within 30 minutes, and now when the site is loaded, that sweet "https" is appended to the front of the url. It's worth noting that to maintain the cert costs $0.54 per month after taxes. The padlock and feeling of safety my visitors get is well worth it. 

# What's Next?

The website is live and living up to my expectations fully. I'm no less busy than I was when I first began, so small incremental updates is my goal. A nice blog post here and there could be nice. Also, I am working with a couple classmates to develop a full stack application, and this website should be a handy place to deploy it to, using more AWS products. Thanks for stopping by.