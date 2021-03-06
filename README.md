# dsosiso-apps
การสร้างแอพพิเคชั่นDSOSIOS APPS
My Apps
All Docs
Web SDKs
JavaScript SDK
Quickstart
Advanced Setup
Examples
Frameworks
Reference
PHP SDK
Docs/Web SDKs/JavaScript SDK/Quickstart/
Basic Setup
Quickstart: Facebook SDK for JavaScript
The Facebook SDK for JavaScript provides a rich set of client-side functionality that:

Enables you to use the Like Button and other Social Plugins on your site.
Enables you to use Facebook Login to lower the barrier for people to sign up on your site.
Makes it easy to call into Facebook's Graph API.
Launch Dialogs that let people perform various actions like sharing stories.
Facilitates communication when you're building a game or an app tab on Facebook.
The SDK, social plugins and dialogs work on both desktop and mobile web browsers.

This quickstart will show you how to setup the SDK and get it to make some basic Graph API calls. If you don't want to setup just yet, you can use our JavaScript Test Console to use all of the SDK methods, and explore some examples (you can skip the setup steps, but the rest of this quickstart can be tested in the console).

Basic Setup
The Facebook SDK for JavaScript doesn't have any standalone files that need to be downloaded or installed, instead you simply need to include a short piece of regular JavaScript in your HTML that will asynchronously load the SDK into your pages. The async load means that it does not block loading other elements of your page.

The following snippet of code will give the basic version of the SDK where the options are set to their most common defaults. You should insert it directly after the opening <body> tag on each page you want to load it:

<script>
  window.fbAsyncInit = function() {
    FB.init({
      appId            : 'your-app-id',
      autoLogAppEvents : true,
      xfbml            : true,
      version          : 'v2.11'
    });
  };

  (function(d, s, id){
     var js, fjs = d.getElementsByTagName(s)[0];
     if (d.getElementById(id)) {return;}
     js = d.createElement(s); js.id = id;
     js.src = "https://connect.facebook.net/en_US/sdk.js";
     fjs.parentNode.insertBefore(js, fjs);
   }(document, 'script', 'facebook-jssdk'));
</script>
    
This code will load and initialize the SDK. You must replace the value in your-app-id with the ID of your own Facebook App. You can find this ID using the App Dashboard.

Next Steps

Quickstart: Facebook SDK for JavaScript
The Facebook SDK for JavaScript provides a rich set of client-side functionality that:

Enables you to use the Like Button and other Social Plugins on your site.
Enables you to use Facebook Login to lower the barrier for people to sign up on your site.
Makes it easy to call into Facebook's Graph API.
Launch Dialogs that let people perform various actions like sharing stories.
Facilitates communication when you're building a game or an app tab on Facebook.
The SDK, social plugins and dialogs work on both desktop and mobile web browsers.

This quickstart will show you how to setup the SDK and get it to make some basic Graph API calls. If you don't want to setup just yet, you can use our JavaScript Test Console to use all of the SDK methods, and explore some examples (you can skip the setup steps, but the rest of this quickstart can be tested in the console).

Basic Setup
The Facebook SDK for JavaScript doesn't have any standalone files that need to be downloaded or installed, instead you simply need to include a short piece of regular JavaScript in your HTML that will asynchronously load the SDK into your pages. The async load means that it does not block loading other elements of your page.

The following snippet of code will give the basic version of the SDK where the options are set to their most common defaults. You should insert it directly after the opening <body> tag on each page you want to load it:

<script>
  window.fbAsyncInit = function() {
    FB.init({
      appId            : 'your-app-id',
      autoLogAppEvents : true,
      xfbml            : true,
      version          : 'v2.11'
    });
  };

  (function(d, s, id){
     var js, fjs = d.getElementsByTagName(s)[0];
     if (d.getElementById(id)) {return;}
     js = d.createElement(s); js.id = id;
     js.src = "https://connect.facebook.net/en_US/sdk.js";
     fjs.parentNode.insertBefore(js, fjs);
   }(document, 'script', 'facebook-jssdk'));
</script>
    
This code will load and initialize the SDK. You must replace the value in your-app-id with the ID of your own Facebook App. You can find this ID using the App Dashboard.
JavaScript SDK - Advanced Setup
Read our quickstart guide to learn how to load and initialize the Facebook SDK for JavaScript. While the quickstart will use common defaults for the options available when initializing the SDK. You can customize some of these options.

Changing the Language
In the basic setup snippet, the en_US version of the SDK is initialized, which means that all of the Facebook-generated buttons and plugins used on your site will be in US English. (However, pop-up dialogs generated by Facebook like the Login Dialog will be in the language the person has chosen on Facebook, even if they differ from what you've selected.) You can change this language by changing the js.src value in the snippet. Take a look at Localization to see the different locales that can be used. For example, if your site is in Spanish, using the following code to load the SDK will cause all Social Plugins to be rendered in Spanish.

<script>
  (function(d, s, id){
     var js, fjs = d.getElementsByTagName(s)[0];
     if (d.getElementById(id)) return;
     js = d.createElement(s); js.id = id;
     js.src = "https://connect.facebook.net/es_LA/sdk.js";
     fjs.parentNode.insertBefore(js, fjs);
   }(document, 'script', 'facebook-jssdk'));
</script> 
Login Status Check
If you set status to true in the FB.init() call, the SDK will attempt to get info about the current user immediately after init. Doing this can reduce the time it takes to check for the state of a logged in user if you're using Facebook Login, but isn't useful for pages that only have social plugins on them.

You can use FB.getLoginStatus to get a person's login state. Read on for more about using Facebook Login with the JavaScript SDK.

Disabling XFBML Parsing
With xfbml set to true, the SDK will parse your page's DOM to find and initialize any social plugins that have been added using XFBML. If you're not using social plugins on the page, setting xfbml to false will improve page load times. You can find out more about this by looking at Social Plugins.

Triggering Code when the SDK loads
The function assigned to window.fbAsyncInit is run as soon as the SDK has completed loading. Any code that you want to run after the SDK is loaded should be placed within this function and after the call to FB.init. Any kind of JavaScript can be used here, but any SDK functions must be called after FB.init.

Debugging
To improve performance, the JavaScript SDK is loaded minified. You can also load a debug version of the JavaScript SDK that includes more logging and stricter argument checking as well as being non-minified. To do so, change the js.src value in your loading code to this:

js.src = "https://connect.facebook.net/en_US/sdk/debug.js";
More Initialization Options
The reference doc for the FB.init function provides a full list of available initialization options.
JavaScript SDK - Examples
Read our quickstart guide to learn how to load and initialize the Facebook SDK for JavaScript and our advanced setup guide to customize your implementation. Next try our examples for using the SDK:

Trigger a Share dialog
Facebook Login
Call the Graph API
Trigger a Share dialog
The Share Dialog allows someone using a page to post a link to their timeline, or create an Open Graph story. Dialogs displayed using the JavaScript SDK are automatically formatted for the context in which they are loaded - mobile web, or desktop web.

Here we'll show you how the FB.ui() method of the SDK can be used to invoke a really basic Share dialog. Add this snippet after the FB.init() call in the basic setup code:

FB.ui(
 {
  method: 'share',
  href: 'https://developers.facebook.com/docs/'
}, function(response){});
Now when you reload your page, you'll see a Share dialog appear over the top of the page. Let's add a few extra parameters to the FB.ui call in order to make the Share dialog make a more complex call to publish an Open Graph action:

FB.ui({
  method: 'share_open_graph',
  action_type: 'og.likes',
  action_properties: JSON.stringify({
    object:'https://developers.facebook.com/docs/',
  })
}, function(response){
  // Debug response (optional)
  console.log(response);
});
Now when you reload your page, you'll see a Share dialog again, but this time with a preview of the Open Graph story. Once the dialog has been closed, either by posting the story or by cancelling, the response function will be triggered.

Read the FB.ui reference doc to see a full list of parameters that can be used, and the structure of the response object.

Read `FB.ui` Reference Documentation
Facebook Login
Facebook Login allows users to register or sign in to your app with their Facebook identity.

We have a full guide on how to use the JS SDK to implement Facebook Login. But for now, let's just use some basic sample code, so you can see how it works. Insert the following after your original FB.init call:

FB.getLoginStatus(function(response) {
  if (response.status === 'connected') {
    console.log('Logged in.');
  }
  else {
    FB.login();
  }
});
Read the Login guide to learn exactly what is happening here, but when you reload your page you should be prompted with the Login dialog for you app, if you haven't already granted it permission.

Learn more about Facebook Login
Call the Graph API
To read or write data to the Graph API use method FB.api(). The version parameter in the FB.init call is used to determine which Graph API version is used.

Login Button & Requesting Permissions
First, get the publish_actions permission to make publishing API calls. Add a button or a link calling FB.login. This will trigger a login dialog that'll request the relevant permissions.

<script>
// Only works after `FB.init` is called
function myFacebookLogin() {
  FB.login(function(){}, {scope: 'publish_actions'});
}
</script>
<button onclick="myFacebookLogin()">Login with Facebook</button>
Graph API Call
Let's make an API call to publish a message. Add the code into the response function of the FB.login call you added above:

FB.login(function(){
  // Note: The call will only work if you accept the permission request
  FB.api('/me/feed', 'post', {message: 'Hello, world!'});
}, {scope: 'publish_actions'});
Try the script. A status message will be posted to your timeline:
Framework Guides for the JavaScript SDK
AngularJS
Concepts how to integrate the Facebook SDK for JavaScript in your AngularJS app.

jQuery
Incorporate the Facebook SDK for JavaScript into your jQuery-based web app.

RequireJS
Incorporate the Facebook SDK for JavaScript with other JavaScript modules using RequireJS.
Facebook SDK for JavaScript with AngularJS

You can integrate the Facebook SDK for JavaScript with AngularJS. However as our SDK has to work for the web and not for a particular framework, we do not offer a AngularJS module.

Loading the Facebook SDK for JavaScript
For adding the Facebook SDK for JavaScript to your app we recommend to follow the how-to Facebook authentication in your AngularJS web app or other guides posted on https://docs.angularjs.org/guide.

Use the latest SDK Version
When following any guide please make sure to load the latest SDK file sdk.js:

// Old SDK (deprecated)
js.src = "https://connect.facebook.net/en_US/all.js";

// New SDK (v2.x)
js.src = "https://connect.facebook.net/en_US/sdk.js";
and provide a Graph API version (currently v2.4) in the FB.init() call:

$window.fbAsyncInit = function() {
    FB.init({ 
      appId: '{your-app-id}',
      status: true, 
      cookie: true, 
      xfbml: true,
      version: 'v2.4'
    });
};
Handling Callbacks
The Facebook SDK for JavaScript does not support the concept of promises. As a workaround you can bundle your Facebook for JavaScript SDK calls (for example) into a service:

// ...
.factory('facebookService', function($q) {
    return {
        getMyLastName: function() {
            var deferred = $q.defer();
            FB.api('/me', {
                fields: 'last_name'
            }, function(response) {
                if (!response || response.error) {
                    deferred.reject('Error occured');
                } else {
                    deferred.resolve(response);
                }
            });
            return deferred.promise;
        }
    }
});
Use the service for example like this:

$scope.getMyLastName = function() {
   facebookService.getMyLastName() 
     .then(function(response) {
       $scope.last_name = response.last_name;
     }
   );
};
Third Party Libraries
There are also several third party libraries simplifing the usage of the Facebook SDK for JavaScript listed on the AngularJS Guide page.
Facebook SDK for JavaScript with jQuery
In this tutorial, you’ll learn how to incorporate the Facebook JavaScript SDK into your jQuery-based web app. Both jQuery and the JavaScript SDK provide their own solutions for deferring code execution until the libraries have loaded, and this tutorial will help you combine the two and ensure both are ready to use before you invoke the SDK.

This example uses jQuery 2.0.0 served from Google’s Hosted Libraries CDN. To find out more about jQuery, take a look at the jQuery Documentation

Implementation
Add jQuery to your document head, and implement the $(document).ready() method, which will execute when the DOM is complete and jQuery is instantiated. Your page will look something like this:

<html>
<head>
  <script src="//ajax.googleapis.com/ajax/libs/jquery/2.0.0/jquery.min.js"></script>
  <link rel="stylesheet" href="style.css" />
  <title>jQuery Example</title>
  <script>
    $(document).ready(function() {
      // Execute some code here
    });
  </script>
</head>
Instead of importing the Facebook JavaScript SDK with the default async script, use jQuery’s getScript() method to import the SDK from the correct URL for your user’s locale. You can leave out the protocol from the beginning of the URL, and this will serve a matching protocol for the current URL.

By default, jQuery timestamps asynchronous requests to avoid them being cached by the browser. You’ll want to disable this functionality using the ajaxSetup() method, so that the SDK is cached locally between pages.

The getScript() method is asynchronous, so you’ll pass an anonymous callback function in which you can do your SDK initialization code as usual. Add the App ID for your app from the App Dashboard.

$(document).ready(function() {
  $.ajaxSetup({ cache: true });
  $.getScript('//connect.facebook.net/en_US/sdk.js', function(){
    FB.init({
      appId: '{your-app-id}',
      version: 'v2.7' // or v2.1, v2.2, v2.3, ...
    });     
    $('#loginbutton,#feedbutton').removeAttr('disabled');
    FB.getLoginStatus(updateStatusCallback);
  });
});
Dependency Decoupling
Putting all your SDK invocation logic in the getScript callback will guarantee that the FB object exists, but it’s not a great design pattern for a complex app. Since the FB object is global, you can put SDK logic outside the getScript callback as long as you check that it exists before calling it. Alternatively, you can use a module dependency framework such as RequireJS to ensure that the FB object is loaded as part of application setup.

See Also
JavaScript SDK Reference
Use the JavaScript SDK with RequireJS
Facebook SDK for JavaScript with RequireJS
In this tutorial, you'll learn how to incorporate the Facebook SDK for JavaScript with other JavaScript modules using RequireJS. Ordinarily, the JavaScript SDK isn’t compatible with the Asynchronous Module Definition (AMD) design pattern, so this tutorial covers writing a shim to provide the FB object created by the SDK.

This tutorial assumes you’re familiar with RequireJS and JavaScript modules. Find out more about RequireJS.

Configuration
Configure your other RequireJS scripts as normal, and add a new .js file for interaction with the Facebook SDK. This project assumes a directory structure like the one below:

- project/
   - index.html
   - scripts/
      - main.js
      - require.js
Add a new file for configuring and interacting with the SDK, as below:

- project/
    - index.html
    - scripts/
       - main.js
       - require.js
       - fb.js
You should be importing the requirejs script and declaring main.js as your data-main as follows:

<script data-main="scripts/main" src="scripts/require.js"></script>
Adding a shim to the Facebook SDK
In your main project script, add a shim declaration to the require.config, as shown:

require.config({
  shim: {
    'facebook' : {
      exports: 'FB'
    }
  },
  paths: {
    'facebook': '//connect.facebook.net/en_US/sdk'
  }
})
require(['fb']);
This creates a facebook module, using the JavaScript SDK URL, and marks the FB object as the export for that module. Notice that we don't specify a protocol (HTTP or HTTPS) when adding the SDK URL, which ensures that it will match the protocol of the current page.

In your newly-created fb.js, you can instantiate and use the FB object as usual. Add the App ID for your app from the App Dashboard.

You just need to wrap your code in a define block, passing the facebook shim module as a required dependency.

define(['facebook'], function(){
  FB.init({
    appId      : '{your-app-id}',
    version    : 'v2.11'
  });
  FB.getLoginStatus(function(response) {
    console.log(response);
  });
});
See Also
Getting Started with the Facebook SDK for JavaScript
JavaScript SDK Reference

