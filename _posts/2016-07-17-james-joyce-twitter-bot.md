---
layout: post
section-type: post
title: Python twitter bot
category: python 
tags: 
---
It's been said that James Joyce's lengthy novel *Ulysses* is so cryptic and oftentimes confusing, that the reader could spend a lifetime opening the book at random, always finding a new perspective. Though a number of Twitter accounts already tweet in 140 character blocks of text, I felt there to be a gap for a new approach: retaining the novel's pre-existing formatting by imposing each text excerpt on an image.	

The task of drawing text to images was facilitated by the Python Imaging Library.
I was able to source a Joyce portrait under a Universal Creative Commons license from [archive.org](https://archive.org/details/JamesJoyceVariousPhotos), while the text to Ulysses is freely available at [gutenberg.org](http://www.gutenberg.org/ebooks/4300). Similiary, Twitter's vector logos and branding guidelines are freely available at [brand.twitter.com](https://brand.twitter.com/).

In one sense the very act of tweeting a 96-year old novel via Twitter was a clashing of worlds, Twitter users had many distractions so I had to get to the point. It was tempting to fit 500+ words in a single tweet, but this was refined so as to offer short easily-scannable passages which could be quikly skimmed

The project is hosted on an AWS EC2 instance, running on a cronjob every 3 hours.
The twitter account can be viewed at [twitter.com/randomUlysses](https://twitter.com/randomUlysses)
The Git repository for this project can be viewed [here](https://github.com/oisinBates/JamesJoyceUlyssesTwitterBot)
