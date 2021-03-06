#iOStream

Presenting mobile apps is a pain in the ass. So is collaborating remotely with mobile developers. Don't let clunky hardware cameras and unrealistic simulators get in your way. Introducing <a href="http://iostream.io">iOStream</a>. Mobile presentations made easy. Install the SDK and start streaming now.

## About

iOStream was created by <a href="https://github.com/thecalvinchan/">Calvin Chan</a>, <a href="https://github.com/shenil">Shenil Dodhia</a>, <a href="https://github.com/earllee">Earl Lee</a>, and <a href="https://github.com/johnmoore">John Moore</a> at the PennApps Spring 2014 hackathon over the course of 36 hours.

## Installation

In order to use iOStream, you must link your application with libicucore.dylib, CFNetwork.framework, and Security.framework. Then import the folder /sdk/iOStreamClient into your XCode project, and add the following code to your application delegate files:

(In AppDelegate.h)
```objective-c
#import "iOStream.h"
```

(In AppDelegate.m)
```objective-c
- (BOOL)application:(UIApplication *)application didFinishLaunchingWithOptions:(NSDictionary *)launchOptions
{
    // Override point for customization after application launch.
    // (Your code here . . .)

    iOStreamClient *client = [iOStreamClient sharedInstance];
    client.frameInterval = 6; //10 FPS
    client.showsTouchPointer = YES; //show the touch pointer
    [client startStream];
    
    return YES;
}
```

## View or share your app's stream

You will be given a unique code every time you launch your app. Share your code with others to allow them to view your app's stream.

You can enter a code at http://iostream.io/stream.html. For sharing codes, you can set the "channel" GET variable as shown below. Be sure to replace XXXXXXXX with the code you receive from your app.

> http://iostream.io/stream.html?channel=XXXXXXXX

## Host your own version

You can host your own version using the Node.js server in the /server folder of this repo. You will need to use npm to install the necessary modules if you haven't already. Then, edit sdk/iOStreamClient/iOStream.m to point to your server:

```objective-c
NSString * const host = @"api.yourhost.com";
```

You will need to host the web app component as well. The source is located under the /website directory. Please note that you will need to edit /website/assets/js/main.js to connect to your own server instead of ours:

```javascript
var socket = new io.connect('http://yourhost:2000'); 
```

## Fork it!

We welcome your help in improving iOStream. It started as a quick-and-dirty hackathon project and proof of concept, and we'd love to see what the community does with it.

## License

We are releasing iOStream (website, server, and iOS SDK) under the <a href="http://opensource.org/licenses/RPL-1.5">Reciprocal Public License v1.5</a>. You are free to do what you want with the source, but we ask that you release any modified versions as open-source software to the public.

Thanks to Philipp Kyeck (http://beta-interactive.de) for the Objective-C iOS library and Kishikawa Katsumi (http://kishikawakatsumi.com/) for the initial basis of the screen-recording iOS code, both of which were licensed under the MIT license (see /sdk for a copy).
