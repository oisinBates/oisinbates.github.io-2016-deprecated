---
layout: post
section-type: post
title: Python twitter bot
category: python 
tags: 
---
It's been said that James Joyce's lengthy novel *Ulysses* is so cryptic and oftentimes confusing, that the reader could spend a lifetime opening the book at random, always finding a new perspective. Though a number of Twitter accounts already tweet in 140 character blocks of text, I felt there to be a gap for a new approach: tweeting short sections text as the novel's pre-existing formatting by imposing each text excerpt on an image.	

While the use of an image - over a standard 140-character tweet -offered the ability to tweet many hundereds of words in a single tweet, I determined it better to stick with large text in the novels original formatting. One distinct advantage of this was the ability to retain the formatting of dialogues, as opposed to other twitterbots which mash all lines into a single 140-character block.

Though image tweets offered greater flexibility in formatting text, it was still important to ensure easy readability. As of such, though it was possible to print many hundreds of words to a single image, I reasoned it wiser to print around 50; aiming to make it easily accessible to those skimming their Twitter feeds.

The process of writing text to images was facilitated by the Python Imaging Library, while the *Tweepy* API facilitated the task of uploading to Twitter.
Joyce portraits can be sourced under a Universal Creative Commons license from [archive.org](https://archive.org/details/JamesJoyceVariousPhotos), while the text of Ulysses is freely available at [gutenberg.org](http://www.gutenberg.org/ebooks/4300). Similiary, Twitter's vector logos and branding guidelines are freely available at [brand.twitter.com](https://brand.twitter.com/).

The project is hosted on an AWS EC2 instance, running on a cron job so as to tweet every 3 hours.
The twitter account can be viewed at [twitter.com/randomUlysses](https://twitter.com/randomUlysses)
The Git repository for this project can be viewed [here](https://github.com/oisinBates/JamesJoyceUlyssesTwitterBot).
