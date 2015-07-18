## Example project showing audio streaming using HTML5 Audio with PhoneGap on iOS


### Why is this here?

I was working on a radio streaming app in PhoneGap and due to a bug in the PhoneGap iOS Media API decided to create a plugin to handle the audio streaming based on the native code I had used in the previous version of the app before discovering PhoneGap.

I got 98% of the way there with my plugin, but in the end it turned out to just be a million times simpler to use html5 audio (`new Audio()`) to do the streaming in my radio app.

Since shipping that app and effectively abandoning my plugin, I have received a great deal of queries about the plugin and its example project. I have been answering these by pointing people at the web page that got me started using html5 audio nin PhoneGap: http://www.joeldare.com/wiki/play_an_mp3_audio_stream_in_phonegap

However, this is a bit of a cop out... so I decided to re-write my example audio streaming app using the html5 audio instead of my plugin.

Here it is.

### Notes

#### PhoneGap/Cordova

As no PhoneGap API's are used... just pure JavaScript, there is no PhoneGap / Cordova project included. Feel free to just use the contents of the `www` folder in a new project instead.

#### Background Audio

If you need background audio, you will need to add the supported modes in your `<Projectname>-info.plist` (in this case, `ExampleHTML5AudioStreaming-Info.plist`):

	<key>UIBackgroundModes</key>
    	<array>
        	<string>audio</string>
    	</array>

Also important to note, since iOS6, you must explicitly set the AVAudioSessionCategory.

http://stackoverflow.com/a/12414719/878602

First, import AVFoundation into your `AppDelegate.m` `#import <AVFoundation/AVFoundation.h>`

Then add the following to `application:(UIApplication*)application didFinishLaunchingWithOptions:(NSDictionary*)launchOptions`

```objective-c
AVAudioSession *audioSession = [AVAudioSession sharedInstance];
BOOL ok;
NSError *setCategoryError = nil;
ok = [audioSession setCategory:AVAudioSessionCategoryPlayback error:&setCategoryError];
```

*It is also important to note that background audio does* **not** *work in the iOS Simulator...* **only** *on an actual device*

## License

The MIT License

Copyright (c) 2011 Tommy-Carlos Williams (github.com/devgeeks)

Permission is hereby granted, free of charge, to any person obtaining a copy of this software and associated documentation files (the "Software"), to deal in the Software without restriction, including without limitation the rights to use, copy, modify, merge, publish, distribute, sublicense, and/or sell copies of the Software, and to permit persons to whom the Software is furnished to do so, subject to the following conditions:

The above copyright notice and this permission notice shall be included in all copies or substantial portions of the Software.

THE SOFTWARE IS PROVIDED "AS IS", WITHOUT WARRANTY OF ANY KIND, EXPRESS OR IMPLIED, INCLUDING BUT NOT LIMITED TO THE WARRANTIES OF MERCHANTABILITY, FITNESS FOR A PARTICULAR PURPOSE AND NONINFRINGEMENT. IN NO EVENT SHALL THE AUTHORS OR COPYRIGHT HOLDERS BE LIABLE FOR ANY CLAIM, DAMAGES OR OTHER LIABILITY, WHETHER IN AN ACTION OF CONTRACT, TORT OR OTHERWISE, ARISING FROM, OUT OF OR IN CONNECTION WITH THE SOFTWARE OR THE USE OR OTHER DEALINGS IN THE SOFTWARE.
