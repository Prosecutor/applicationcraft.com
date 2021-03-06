---
title: Amazingly Easy Authentication with OAuth
author: Freddy May
tags: oauth, authentication, twitter, facebook, dropbox
date: 2012-12-04
class_name: blog
image: blog/oauth.png
full_width: true
---

We recently added [OAuth](http://oauth.net/) support to Application Craft, and in the usual Application Craft way, we've made it amazingly simple.

We currently provide explicit support for Twitter, Facebook and Dropbox but we'll soon be adding support for more OAuth providers, as well as allowing you to make your own OAuth definitions so any service that supports OAuth can be defined in the AC Console.

##Authentication for your Apps
One of the simpler uses for OAuth is to provide access to your App. You let a 3rd party service like Twitter or Facebook handle the login process.

Authentication is as easy as shown below. You call `OAuthSignIn()` and that's it. The service pops up in a browser window, handles the login and returns an access token. You can store that token in a cookie so when your users access your App in the future, they don't have to login again (until the service decides to expire it).

    function handler_btnAuth_onClick(mouseev){
      // See if we already have an old Access Token
      _accessToken = app.getCookie("myTwitterSession");
      if (_accessToken === null || _accessToken === "") {
        // No, we don't have one so get a new one
        app.OAuthSignIn('twitter', authCallback);
      }
    }


##Calling OAuth secured APIs
Things get much more interesting when you want to access APIs from services such as Twitter, Facebook and Dropbox. Using our OAuth support, you can access the full functionality of those services in a way that is remarkably easy.

This short example shows the code for sending a Tweet via Twitter. It is actually made up of two parts - the code running on the client ...

	function handler_btnTweet_onClick(mouseev){
		app.callSSJ('sendTweet', function(error, data){
      if(error) {
      	// Some error occurred (maybe the 
      	// Access Token has expired)
      } else {
        app.showMessage("OAuth Demo", "Message successfully tweeted!");  
      }
    }, [_accessToken, txtTweetMessage]);
	}

... and the server side code that gets called by `app.callSSJ()` in the above example.

	function sendTweet(accessToken, txtTweet) {
    ssj.OAuthRequest(accessToken, 
        'https://api.twitter.com/1.1/statuses/update.json',    
        'POST', { status: txtTweet });
	}

Have you ever seen OAuth handled that straightforward? Application Craft does all the dirty work and heavy lifting for you.

##Read the Documentation
[Click here](/developers/documentation/product-guide/advanced-features/oauth/) to read the OAuth documentation in the Product Guide.



