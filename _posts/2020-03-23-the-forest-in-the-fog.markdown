---
layout: post
title: The forest in the fog.
date: 2020-03-23 05:18:20 +0300
description: Web Workers are, undoubtedly, the coolest feature to stumble upon in this programming quest.
img: the_forest_in_the_fog/header.png # Add image post (optional)
tags: [Programming, JavaScript]
category: [Programming]
author: # Add name author (optional)
---
`This entire blog, especially the title and the context below, is non-normative.`

I hope you're staying safe fam, what with all these COVID - 19 cases going around. Corona is real, stay woke 🖖, stay clean, most importantly, **Stay At Home**. Need I say more?

Recently, I had to build a react app. (That is why I haven't written in a while, redux is hard to master for me). 
I got a bug and decided to work on Doodle to ease my mind off the pressure.

[Doodle](https://newtonkaranu.me/doodle/){:target="_blank"}, the pet project, is basically an app that draws random lines and gives you the option to export them as either svg or png.
I thought to update it to add an option of exporting a gif, cause I used it to understand svg and png images and how they are made, so why not understand gifs as well?

**NB:** As of publishing this post, the doodler does not have the gif downloader yet because I encountered bugs as I tried to update the worker. Will update this note once the gif downloader is up and running.😅😅 _You're probably wondering what worker is, read on..._

For the record, I got the inspiration for the pet project from doodling on paper.
![Real Doodle](/blog/assets/img/the_forest_in_the_fog/doodle.jpeg)

I discovered [JSGif](https://github.com/antimatter15/jsgif), a port of as3gif GIFPlayer(AS3GIF lets you play and encode animated GIF's with ActionScript 3) to JS.

While the tool did work, it slowed down the ui component (the canvas) where I was drawing the doodles. It wasn't as fast as I would like. After doing some research, 
I found out that JavaScript single threaded.
> Well, if you see from the under hood working of browser JS to your JS code, there are thread pools. <br>
By single threaded what they mean(browser end) is your JS runs into a single threaded event loop. <br>
There is one single thread that handles your event loop. <br>
Under your JS, the browser code is running multiple threads to capture events and trigger handlers, when they capture any new event, they push it on an event queue and then that event loop,
 in which your code is running gets triggered and it handles the request
 
#### TL;DR 
Your JavaScript code is single-threaded in the same context, but all other stuff which is done by browser (AJAX request, rendering, event triggers etc.) is not.

I had to find a way to save my gifs without slowing down the event loop.

## Computing with JavaScript Web Workers
Then I discovered web workers.

Web Workers allow you to run JavaScript in parallel on a web page, without blocking the user interface.

Normally in order to achieve any sort of computation using JavaScript you would need to break your jobs up into tiny chunks and split their execution apart using timers.

A `worker` is a script that will be loaded and executed in the background. Workers (as these background scripts are called herein) are relatively heavy-weight, and are not intended to be used in large numbers.
Generally, workers are expected to be long-lived, have a high start-up performance cost, and a high per-instance memory cost.

The way to create gifs without using a web worker looked something like this.

{% highlight javascript %}
// my js file index.js
......
function btSaveGifHandler(e) {
    saveGIF('Doodle.gif')
}

function saveGIF (name) {

    setTimeout(function() { // give external JS 1 second of time to load

        console.log('Starting');
            // getting the canvas being drawn
            var canvas = document.getElementBygetElementsByName(canvas);
            // getting the stuff being drawn inside the canvas
            var context = canvas.getContext('2d');
            var grabLimit = 60;  // Number of screenshots to take
            var grabRate  = 270; // Miliseconds. 500 = half a second
            var count     = 0;
        
            function showResults() {
                console.log('Finishing'); // sprinke console logs here and there to see what is happening
                 encoder.finish();
                 encoder.download("download.gif"); // download the gif
            }
        
            var encoder = new GIFEncoder();
            encoder.setRepeat(0);  //0  -> loop forever, 1+ -> loop n times then stop
            encoder.setDelay(0); //go to next frame every n milliseconds
            encoder.start();
        
            var grabber = setInterval(function(){
            console.log('Grabbing '+count);
            count++;
        
            if (count>grabLimit) {
                clearInterval(grabber);
                showResults();
              }
              
             encoder.start();
             encoder.addFrame(context);
        
            }, grabRate);

    }, 1000);
}
......
{% endhighlight %}

Now, the better way, to create gifs without blocking the doodle the user is seeing is by using workers.

**NB:** workers don’t have access to the DOM. No document, getElementById, etc. (The notable exceptions are setTimeout, setInterval, and XMLHttpRequest.)

You use a worker by communicating with it using messages. All browsers support passing in a string message (Firefox 3.5 also supports passing in JSON-compatible objects). 
This message will be communicated to the worker (the worker can also communicate messages back to the parent page). This is the extent to which communication can occur.

{% highlight javascript %}
// my js file index.js
......
btSaveGIF = document.getElementById('btSaveGIF');
btSaveGIF.addEventListener('mousedown', btSaveGifHandler, false);

function btSaveGifHandler(e) {
    // Watch for messages from the worker
    worker.onmessage = function(e){
      // The message from the client:
      if ( e.data === "done" ) {
      console.log('Finshed creating and downloading the gif'); // sprinke console logs here and there to see what is happening
      }
    };
    var worker = new Worker('/path_to_/worker.js');
    worker.postMessage("startCreatingGif"); // pretty self explanatory
}
......
{% endhighlight %}

And the worker itself:
{% highlight javascript %}
// my worker js file /path_to_/worker.js
onmessage = function(e){
  if ( e.data === "startCreatingGif" ) {
    setTimeout(function() { // give external JS 1 second of time to load
    
        console.log('Starting');
            // getting the canvas being drawn
            var canvas = document.getElementBygetElementsByName(canvas);
            // getting the stuff being drawn inside the canvas
            var context = canvas.getContext('2d');
            var grabLimit = 1000;  // Number of screenshots to take
            var grabRate  = 270; // Miliseconds. 500 = half a second
            var count     = 0;
        
            function showResults() {
                console.log('Finishing'); // sprinke console logs here and there to see what is happening
                 encoder.finish();
                 encoder.download("download.gif"); // download the gif
            }
        
            var encoder = new GIFEncoder();
            encoder.setRepeat(0);  //0  -> loop forever, 1+ -> loop n times then stop
            encoder.setDelay(0); //go to next frame every n milliseconds
            encoder.start();
        
            var grabber = setInterval(function(){
            console.log('Grabbing '+count);
            count++;
        
            if (count>grabLimit) {
                clearInterval(grabber);
                showResults();
              }
              
             encoder.start();
             encoder.addFrame(context);
        
            }, grabRate);

    }, 1000);
    
    done()
  }
};
 
function done(){
  // Send back the results to the parent page
  postMessage("done");
}
{% endhighlight %}

I probably think I could modify this even further so that the worker's work is to only capture the canvas and create the gif. 
Then after the worker is done, I use my js file to publish the gif onto a file then download it.
