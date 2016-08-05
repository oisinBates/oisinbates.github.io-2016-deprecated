---
layout: post
section-type: post
title: bash media timer project
category: bash 
tags: 
---




#### Overview: 
This project was a solution to a personal predicament; I enjoyed the convenience of playing music on a timer via my home stereo, but I often found myself away from home with only my laptop. Of course, there are many possible solutions to this use case, I chose Bash as it offered an opportunity to work with a scripting language which I had not been taught in college.

This script plays radio and music files on a timer as part of a bedtime routine, logging user habits to a MySQL database. It takes two parameters:

$1: Length in minutes for playing radio.

$2: Length of time the user wishes to sleep for(in hours, up to two decimal places permitted).

#### Script Structure:

1. Regular expressions check both paramters to ensure that they are not in violation. Script exits at this point if parameters don't match regexs.
2. Radio begins playing(via google-chrome web browser). Thread sleeps for the period of time specified in $1.
3. Machine suspends to ram for the length of time specified in $2(minus $1).
4. Machine boots up and plays an alarm. A random album of music is queued to play from the local drive.
5. MySQL database updated.

<small>(6). A MySQL event is scheduled to generate weekly averages, which are inserted to a seperate table of averages.</small>

The Git repository for this project can be viewed [here](https://github.com/oisinBates/BashRadioTimerReplacement)