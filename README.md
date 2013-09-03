#HTML5 APIs Workshop

Let's take a look at some interesting APIs that are added with the new [HTML5 specifications](http://www.w3.org/html/wg/drafts/html/master/).

## To be covered

* Fullscreen API

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

First let's add a button to our HTML document for the user to enter full screen mode. Add the following code to our index.html file.

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


