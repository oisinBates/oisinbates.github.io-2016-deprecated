---
layout: post
section-type: post
title: twilio homer simpson autodialer
category: Node.js
tags: 
---

As a big fan of *The Simpsons*, one of my first thoughts upon working with Twilio's API was the potential to re-enact [Homer Simpon's auto-dialer](https://www.youtube.com/watch?v=J-inCB3POqs), and bring a smile to the faces of a small handful of friends who share a love for the cartoon. 
Ultimately it stood as a good excuse to work on a project utilising Twilio's API and a Node.js Express web app. 


The audio file was added to an AWS S3 bucket and made publicly accesible via url. 
I hosted the Express web app via an AWS Ubuntu instance.
The express web app itself held a number of endpoints for all stages of a call's lifecycle.
callbacks to track call status

*With great power, of course, comes great responsibility. I obviously refrained from spamming and only tested the code, for repetitive synchronous calls, on my own phone *

*post in draft stage, more to come
