#HTML5 APIs Workshop

Let's take a look at some interesting APIs that are added with the new [HTML5 specifications](http://www.w3.org/html/wg/drafts/html/master/).

## To be covered

* Fullscreen API
* Link Prefetching
* Geolocation API
* Drag and Drop

## Foundation

The first thing we need is to make sure we are running an HTML5 capabale web browser. You can check out how well your broswer performs [here](http://html5test.com/) and then also check the specific APIs [here](http://caniuse.com/). Make sure your browswer can handle all the APIs that we will be covering in this workshop.

If you think you will run into problems get the latest version of [Chrome](http://www.google.com/chrome).

## Basic template

Listed below is the basic folder structure for this workshop as well as a basic HTML5 compliant structure for a new web page. This is the structure we will base the workshop on. Get familiar with all the basic elements and what they mean.

    folder/
        index.html
        js/
            scripts.js
        css/
            styles.css
    

If you are really clever, you will be able to code this from scratch!

    <!doctype html>
    <html lang="en">
        
        <head>
            <meta charset="utf-8">
            <title>HTML5 API Workshop</title>
            <link rel="stylesheet" href="css/styles.css">
            <!--[if lt IE 9]>
                <script src="http://html5shiv.googlecode.com/svn/trunk/html5.js"></script>
            <![endif]-->
        </head>
        
        <body>
            <script src="js/scripts.js"></script>
        </body>
    
    </html>

## Fullscreen API

This is a JavaScript API that allows developers to launch their web page into full screen in the browser, depending on user approval. This API comes in really handy for making games on the web.

First let's add a button to our HTML document inside the body tag for the user to enter full screen mode. Add the following code to our index.html file.

    <button onclick="launchFullScreen()">Launch Full Screen</button>
    
Next, add the following JavaScript code which does all the heavy lifting to use the full screen API. Add the following code to your js/scripts.js file.

    // Find the right method, call on correct elements
    function launchFullScreen() {
        var element = document.documentElement;
        if (element.requestFullScreen) {
            element.requestFullScreen();
        } else if (element.mozRequestFullScreen) {
            element.mozRequestFullScreen();
        } else if (element.webkitRequestFullScreen) {
            element.webkitRequestFullScreen();
        }
    }
    
Hit the button and see the magic at work!

## Link Prefetching

HTML5 allows you to silently preload sites or images to create a more seamless user experience.

Just add the following to our index.html file somewhere inside the body tag.

    <!-- full page -->
    <link rel="prefetch" href="http://hacksu.cs.kent.edu" />
    
    <!-- just an image -->
    <link rel="prefetch" href="https://pbs.twimg.com/media/BFAtXVcCEAIeMHM.jpg" />
    
## Geolocation API

Ever want to know the precise latitude and longitude of your user? You can now do this with HTML5 with some pure javascript.
    
First let's add a button to our HTML document inside the body tag to request the user's location. Add the following code to our index.html file.

    <button onclick="getLocation()">Get Location</button>
    
Next let's add the JavaScript code to our scripts.js file.

    function getLocation() {
        navigator.geolocation.getCurrentPosition(printCoordinates);
    }
    
    function printCoordinates(position) {
        var latitude = position.coords.latitude;
        var longitude = position.coords.longitude;
        console.log('Latitude: ' + latitude);
        console.log('Longitude: ' + longitude);
    }
    
Load the index.html file and open the developer console to see the location printed!

## Drag and Drop

This is a new standard in HTML5 that allows elements to be drag and droppable. And the beautiful thing is, you don't need any library or external script anymore!

Add the following code to our index.html file:

    <div id="dropper" ondrop="drop(event)" ondragover="allowDrop(event)" style="width:255px;height:255px;padding:10px;border:1px solid black;"></div>

    <img id="dragger" src="http://www.w3.org/html/logo/downloads/HTML5_Logo_512.png" draggable="true" ondragstart="drag(event)" width="250" height="250">

Next, add the following JavaScript code to your js/scripts.js file.

    function allowDrop(event) {
	    event.preventDefault();
    }

    function drag(event) {
	    event.dataTransfer.setData("Text",event.target.id);
    }

    function drop(event) {
	    event.preventDefault();
	    var data = event.dataTransfer.getData("Text");
	    event.target.appendChild(document.getElementById(data));
    }

Check it out! Now you can drag the image into the box :)

## Get User Media API

This little tutorial will allow you to capture video directly from your computer's webcam! First let's add a couple elements to our body tag in index.html.

NOTE: This can not be run locally, use Brackets to run a local server with Chrome.

	<video autoplay></video>
	
Now let's get juicy and write some lines of sweet JavaScript code. Add this to your js/scripts.js file.

	var video = document.querySelector('video');

	navigator.getMedia = ( navigator.getUserMedia ||
	                       navigator.webkitGetUserMedia ||
	                       navigator.mozGetUserMedia ||
	                       navigator.msGetUserMedia);
	
	navigator.getMedia (
	
	   // constraints
	   {
	      video: true
	   },
	
	   // successCallback
	   function(localMediaStream) {
	      video.src = window.URL.createObjectURL(localMediaStream);
	      video.onloadedmetadata = function(e) {
	         // Do something with the video here.
	      };
	   },
	
	   // errorCallback
	   function(err) {
	    console.log("The following error occured: " + err);
	   }
	);

Now you must be wondering what this code means...
