---
title: Why I Chose Ghost Over Wordpress
date: 2018-07-14 17:51:46
updated: 
type: post
tags: [ghost, wordpress]
---

There's plenty of posts out on the web like this, and I'm adding to the mass! Last weekend I switched my blog from the, in my opinion, not-so-cool anymore _WordPress_ to a hip, relatively new blogging platform that goes by the name of _Ghost_. To do that, I also took the plunge and decided to make use of my long standing $10 credit with _Digital Ocean_ and decided to host my blog entirely on one of their VPS's which they affectionately call _droplets_.

Although Ghost offer a hosted service, one in which they take care of the backend for you, I couldn't convince Mrs Price to let me spend that much, and honestly, I want to maintain it myself (famous last words).

Ghost is open source, and the VPS costs just $5 a month. Which I think is superb. For that I get a VPS with the following specs:

> - 1 vCPU
> - 1GB RAM
> - 25 GB SSD storage space
> - 1 TB bandwidth
> 
> [Pricing @ DigitalOcean](https://www.digitalocean.com/pricing/)

Pretty decent and at the moment more than enough for my needs. It's a great price, offers flexible and affordable scalability and gives me all the freedom I need.

The VPS I've spun up is running Ubuntu 16.04, which is Ghost's recommended OS and the only OS you'll get support from them for.

I do however have a local development environment on my Windows 10 laptop, for theme and design work (despite the Ubuntu support requirement, Windows runs Ghost without any issues), and I've also installed it on a local Ubuntu virtual machine (using Hyper-V) for testing release upgrades and stuff. So, I should be all set.

## Why move from WordPress?

Although I hadn't used WordPress for a few years before starting this blog, very little has changed. You only have to take a look at some of [the themes](https://www.elegantthemes.com/gallery/divi/) you can buy or download for WordPress to see that it's still, in my opinion a bit of a bloated mess. Which is fine, but it's not for me. I want something cleaner and more lightweight.

The process of taking my design for this blog and converting it to WordPress from static HTML was also challenging and frustrating. Things didn't always work, and I never got pagination to work the way I wanted it too, despite lots of research on it (which only told me different things, and didn't solve the problem). You could argue that that's a problem with the user being out of touch with modern HTML/CSS and having little knowledge of PHP rather than the software's problem, but as I mention in a moment, I had no such issues with Ghost.

WordPress is good for a lot of stuff, don't get me wrong. I created a WordPress site for my Dad's church, and despite him not being particularly technically literate he has no problems using it to upload sermons.

I also look after my own church's website, which runs on WordPress as well. It has one of those horribly overcomplicated themes that tries to do too much (I'm not responsible for that decision) so I still very much have a requirement to support and keep up to date with WordPress, but it doesn't mean I have to like it. I used to, but I don't anymore.

Like I say it does have a place, it's opened the door for loads of people, companies, and charities to easily create an online presence, and that's superb, but it's not right for me. It's trying to do too much, it's trying to be so much more than just a blogging platform.

For me, rightly or wrongly, technology is all about the user experience and the feeling I get from a product. Whether it's clean and well built, not just whether it works. WordPress might work, but I hate how over-engineered it feels, and how it tries to do too much, and its reliance on plugins for doing anything you might want to do extra.

## Why Ghost is better

Ghost just isn't like WordPress. Writing in Ghost is two clicks away when you login, and its distraction free. I get to write in Markdown (which I increasingly love), have full control over how my posts are formatted, and can easily add images (drag and drop - in comparison to WordPress' clunky uploader) and generally enjoy the minimalist experience so much more. It allows me to focus on my content, and doesn't get in my way, and it doesn't alter my markup (which happened all the time in WordPress). It's a blogging platform, and doesn't try to be anything more than that. It focuses on its strengths and succeeds.

It's not just the frontend, the backend is equally as impressive. It's so easy to create a theme for in comparison to WordPress. I was able to "port" my blog design in WordPress to Ghost in one afternoon/evening. It took me a few days of frustration with WordPress. Perhaps this is because I was already working with a "mature" design. Whereas, when I initially took my design from static HTML to WordPress a little more work was required? However, I still had to add all the dynamic elements to my design in Ghost, and get my head around what they were actually doing. Despite all that, I had everything done and dusted by late evening - running like a dream.

## Up close with Ubuntu Server

It also gives me a great opportunity to look after running a "production" Linux server. Ok, it's only my blog, but it's still something I need to keep up to date and secure. Some industry experts go with the hosted version of Ghost precisely to avoid this kind of hassle, but I'm quite happy with the "hassle" for now, and if that changes in the future, tough, because Ghost's hosted version will always be too expensive in my opinion! (They recently, as in yesterday, raised their hosted prices significantly - hooray for open source!).

## In Conclusion

Doing all this has left me in a position where I can focus on the content of my blog in a way I couldn't before, little things like that fact that the superb [Unsplash](https://unsplash.com/) is built right in. Which means after my post I can quickly search for, and insert, a featured image. Even things like the fact that it's OpenGraph compatible (social media friendly link previews) without me even having to do anything behind the scenes.

This is stuff that's built in, it's clever, it's been thought through. I don't have to resort to plugins. It's a modern platform built for the age we live in, and I'm happy to be on it.

Thanks for reading.
