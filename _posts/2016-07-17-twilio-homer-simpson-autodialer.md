---
layout: post
section-type: post
title: twilio homer simpson autodialer
category: Node.js
tags: 
---

As a big fan of *The Simpsons*, one of my first thoughts upon working with Twilio's API was the potential to re-create [Homer Simpon's auto-dialer](https://www.youtube.com/watch?v=uGnZMLf5QOI), and bring a smile to the faces of a small handful of friends who share a love for the cartoon.* 
Above all else though, it stood as a good excuse to work on a project utilising a Node.js Express app with Twilio's API. 

The Homer Simpsons soundbite was added to an AWS S3 bucket and made publicly accesible via url. 
The express web app itself, an AWS EC2 Ubuntu instance, facilitated all necessary endpoints the call's lifecycle.
Call status was logged to the console when each call was over 
The express web app itself held a number of endpoints for all stages of a call's lifecycle.
callbacks to track call status
The Git repository for this project can be viewed [here](https://github.com/oisinBates/homerSimpsonAutodialer)

*<i>With great power, of course, comes great responsibility. I obviously refrained from spamming and only tested the code, for repetitive synchronous calls, on my own phone</i>