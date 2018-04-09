---
layout: post
section-type: post
title: Looping & Slowing videos via Youtube's IFrame API
category: javascript
tags:
---

## Introduction
A common method for musicians learning new music is to play along with recordings, isolating short sections and adjusting the tempo if necessary. I have recently been working on a hobby project to curate some of my favourite music by jazz saxophonist Charlie Parker ([charlieparkerlicks.com](charlieparkerlicks.com)). One hurdle to overcome was the copyright associated with directly hosting his recordings. As a consequence, embeded Youtube IFrames proved a good solution. This blog post provides an overview of how I coded my solution and some of the hurdles I faced while doing so. While [I have a running example hosted as a codepen.](https://codepen.io/oisinbates/full/RMYawb) and [Youtube's documentation for their API](https://developers.google.com/youtube/iframe_api_reference) is quite good, this post will provide an abridged overview of the overall codebase.

### Creating the Player
```javascript
function onYouTubeIframeAPIReady() {
  player = new YT.Player('player', {
    height: '270',
    width: '480',
    videoId: '-JKDFD1PZ8Y',
    playerVars: {'controls': 0, 'showinfo': 0, 'modestbranding': 0 },
    events: {
      'onReady': onPlayerReady,
      'onStateChange': onPlayerStateChange
    }
  });
}
```
In creating the player, I chose to specify two events on which I wanted to call functions. The *onReady* event is fired whe the youtube API is ready to begin receiving calls. The *onStateChange* event is fired when the player changes states. In this case the most common states are *playing*, *paused* and *buffering*.

As my use case is looping the audio of a specific tune, I decided to limit the scope of the player's user interface by passing a value of *0* for my chosen properties in the *playerVars* object.

### 'onReady' : Get playback rates and create rate slider
```javascript
function onPlayerReady(event) {
    playbackRates = player.getAvailablePlaybackRates();
    $("#playback-rate-slider").slider({
        min: 0,
        max: playbackRates.length - 1,
        value: [playbackRates.indexOf(1)],
        slide: function(event, ui) {                        
          $('#current-playback-rate').text("Playback Rate: "+ playbackRates[ui.value])
        }       
    });
}
```
In this case, the *player* object is used to call the available playback rates before a slider is created, based on the number of available rates. This is necessary as the number of available playback rates will not always be the same. For example, if the user is on a mobile device, the API will currently only return a single playback rate (1 {Normal}).

While it was sufficient to hard code the range slider for the loop's start and end times, in the case of loading many different videos an obvious benefit would be to access each video's duration via *player.getDuration()*.

### Managing loops with Timeouts
```javascript
var videoIsPlaying = false;
var playbackRates;
var timeoutIds = [];
```
[Timeouts](https://developer.mozilla.org/en-US/docs/Web/API/WindowOrWorkerGlobalScope/setTimeout)
 are essential as they fire the callback necessary to restart each loop.

The biggest design issue surrounded access to click events on the IFrame.
When starting the video by clicking on the IFrame the user can set multiple timeouts,
while in contrast, it is easier to limit timeouts by restricting playback to
the *start* button.

If click events were disabled on the IFrame it would be easier to manage timeout
events as it would only be possible to set a single timeout when clicking the *start*
button. In contrast, when clicking the IFrame, the user can set multiple timeouts.

When each callback is fired, the loop restarts, playing the video with the user's desired start and end point and playback speed. The *playbackRates* variable is used to determine how long the timeout will be, dividing the timeout length by the playback Rate (eg. if playback rate is 2, divide timeout length by 2).

Finally, the *videoIsPlaying* boolean is referenced so as to determine whether to start a new timeout and reset a loop, or not.

### Start / Restart / Stop Looping
```javascript
function startVideo() {
  videoIsPlaying = false;
  player.pauseVideo();

  clearTimeout(timeoutIds[0]);
  timeoutIds.shift();

  let start = $( "#youtube-range-slider" ).slider( "values", 0 );
  let playbackRate = playbackRates[$( "#playback-rate-slider" ).slider( "value" )];
  player.setPlaybackRate(playbackRate);
  player.seekTo(start);
  videoIsPlaying = true;
  player.playVideo();
}
```
*startVideo()* is called when the user starts the video, either by clicking the start button or clicking on the IFrame.


```javascript
function restartVideoSection() {
    timeoutIds.shift();
    let start = $( "#youtube-range-slider" ).slider( "values", 0 );
    player.seekTo(start);
}
```
*restartVideoSection()* is called when the *onStateChange* event is triggered,
the *videoIsPlaying* boolean is true, and there is only one timeout set.

```javascript
function stopVideo() {
  videoIsPlaying = false;
  player.pauseVideo();
  clearTimeout(timeoutIds[0])
  timeoutIds.shift();
}
```
*stopVideo()* stops playback and clears the most recent timeout.

### 'onStateChange' : starting/restarting playback and clearing timeouts
```javascript
function onPlayerStateChange(event) {
  if (event.data == YT.PlayerState.PLAYING) {
    if(!videoIsPlaying || timeoutIds.length > 0){
      if(timeoutIds.length > 0){
        player.pauseVideo();
        //if iframe clicks > 1, multiple timeouts are set
        //clear all timeouts then restart loop
        timeoutIds.map(timeoutID => clearTimeout(timeoutID));  
        timeoutIds=[];
        startVideo();
      }
      else{
        startVideo();
      }
    }
    else{
      //get current playback parameters and restart loop
      let start = $( "#youtube-range-slider" ).slider( "values", 0 );
      let end = $( "#youtube-range-slider" ).slider( "values", 1 );
      let playbackRate = playbackRates[$( "#playback-rate-slider" ).slider( "value" )];
      let duration = ((end - start) / playbackRate) * 1000;

      player.setPlaybackRate(playbackRate);
      timeoutIds.push(window.setTimeout(restartVideoSection, duration));
    }
  }
}
```
This function is called each time the player's state changes.

If the player's state is *playing*, either:
 * Clear timeouts if multiple timeouts are set, and then start videos
 * Else if video is in playing state but the boolean isn't, start video
 * Else if loop has completed and is restarting without issue, get current paramenters
 and restart video

The full, working demo is hosted [here](https://codepen.io/oisinbates/full/RMYawb)
