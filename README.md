# Antourage Widget SDK

## Antourage SDK Functional Description

<img src="./screenshots/image3.png" alt="Screenshots" width="150" />

The Antourage Widget is designed to work as a self-contained ‘widget’ within a host app. Once opened, the widget launches a micro-content vertical that includes live broadcasts and on-demand videos. This content is captured by our mobile Broadcaster application. Antourage is mobile first and designed for the creation and viewing of realtime and near real time micro-content.

<div style="display: flex; justify-content: center; ">
  <img src="./screenshots/image9.png" alt="Screenshots" width="85%"/>
</div>

### Magnetic Widget

The entry point for a user is the magnetic button that appears on the host app. Usually on the main screen, but flexible, the button can appear in more than one place. This magnetic widget can appear in multiple states.

#### "Resting"

<img src="./screenshots/image1.png" alt="Screenshots" width="150" />

If there are no live videos or new VOD’s to watch the widget will be in a “resting” state. When a user clicks the widget in its resting state, they are directed to the main menu of the widget.

#### "LIVE"

<div>
<img src="./screenshots/image12.gif" alt="Screenshots" width="150" />
<img src="./screenshots/image4.png" alt="Screenshots" width="150" />
<img src="./screenshots/image2.png" alt="Screenshots" width="150" />
</div>

When a broadcaster starts streaming live video, the button changes state and animates. The live video can be seen inside the widget and “LIVE” tag appears. If a user taps the widget whilst in this state, they are taken directly to the live broadcast.

#### "NEW"

<img src="./screenshots/image10.gif" alt="Screenshots" width="150" />

When there isn’t a live video, but there are unwatched VOD’s the widget animates with a “NEW” tag. If a user clicks the widget at this point, they will subsequently see the main menu.

### The Main Menu

The main menu allows the user to navigate through multiple live and new videos. Whilst navigating through the videos, if they stop scolling a video will play without sound.  
If a user clicks on the comment or poll icon below any video they will be taken directly to the chat or poll within that video so that they can contribute immediately.  
The main menu can also be customised, by editing the logo in the corner of the screen to surface the organisation or sponsors. The title of the menu can also be customised.

<img src="./screenshots/image11.png" alt="Screenshots" width="40%" />

### Viewing Live Broadcasts

The video player may be used in portrait or landscape mode. In both modes, the viewer can watch the broadcast, see and contribute to comments, and see and respond to polls.

<div>
  <img src="./screenshots/image6.png" alt="Screenshots" width="250" />
  <img src="./screenshots/image5.png" alt="Screenshots" width="500" />
</div>

### Viewing On-demand videos

When the user taps on a video, the video begins playing at the beginning, or if this video has already been partially viewed, it will begin playing at the last point the viewer watched. The Antourage Widget keeps track of which videos the user has seen, and updates the number on the magnetic button accordingly.  
Each video shows the name of the video, name of the broadcaster, total time, and total view count.

### Display Name

In order to contribute to the comments, a user must have an identity in our system, as well as a Display Name that shows in the comments stream. Since not all host apps require a username, we ask users to create a Display Name the first time they try to chat. If the host app does require users to create a username, we can turn off this feature.

### Comments

Comments are contributed by viewers of the live broadcast only. When a video is being watched later as VOD, these comments may be displayed, but cannot be added to. The broadcaster has the ability to review comments on a video and delete ones that they deem to be unacceptable. Antourage administration also has this ability.

### Polls

Polls are created by the broadcaster, and sent out during a live broadcast. They appear on the screen when they are first pushed out to the audience, and viewers can respond or simply close the poll if they do not want to answer. If they answer, they are shown the results right away, and they can see updated results as they come in.  
These polls are sponsorable and images can be uploaded from the web application so that they surface on behalf of all broadcasters. This uploaded images can also be clickable and link to web pages for special offers or further sponsor activation.

<img src="./screenshots/image7.png" alt="Screenshots" width="40%" />

### The Curtain

The curtain feature is supposed to mimic the purpose of a curtain at the theatre. To serve a business purpose such as sponsor exposure or ticket sales, a curtain be lowered at any time. Alternatively, a user can also use the curtain to hide what they are streaming whilst they prepare simulcasts or perform duties off camera.  
Multiple curtains can be uploaded at the same time, therefore different messages/sponsors that you can be ready to raise awareness of when ready. 

<div style="display: flex; justify-content: center; ">
  <img src="./screenshots/image8.png" alt="Screenshots" width="80%"/>
</div>

### Curation

Content can only be created by those who have been actively been given access to stream by the administrator of our partner. Furthermore, with this access, broadcasters can only stream to the specific channels that they have been granted access to stream to. 

### Third Party Technology

To support our functionality, we use a few third-party services and applications.
Firebase: used for push notifications, comments and polls.
Amazon Media Live: used for streaming and hosting our content

## Example

To run the example project, clone the repo, and run

`npm i`

`npx cap sync`

`ionic capacitor run ios --livereload --external`

from the example directory.

## Requirements

iOS 11.3 +  
Android 5+  
[Capacitor](https://capacitorjs.com/docs/getting-started)

## Installation

AntViewer is available through [npm](https://www.npmjs.com). To install
it  run `$ npm install antourage_capacitor`.

### Android additional configuration

1. You should find app build.gradle file and add  `maven { url 'https://jitpack.io' }` to the repositories block.
<img src="./screenshots/android2.png" alt="Screenshots" width="100%" />

2. You should create variable `private AntViewerPlugin antPlugin;`, add `import com.antourage.plugin.AntViewerPlugin;` , `add(AntViewerPlugin.class);` and initialize antPlugin with `antPlugin = (AntViewerPlugin) getBridge().getPlugin(AntViewerPlugin.class.getSimpleName()).getInstance();` in MainActivity class.
Also you need to add `antPlugin.onPause();` and `antPlugin.onResume();` to overriden `onPause` and `onResume` methods accordingly, as you see below:
<img src="./screenshots/android1.png" alt="Screenshots" width="100%" />

`npx cap sync`

`ionic capacitor run android --livereload --external`

## Usage

### Auth

It's static method (no need object init), you can use it anywhere you want (login/app start etc).

``` javascript
import { Plugins } from '@capacitor/core';
const { AntViewerPlugin } = Plugins;

AntViewerPlugin.auth({
        apiKey: "put_your_apiKey_there",
        refUserId: "put_user_id_from_your_base_or_null",
        nickname: "put_user_nickname_from_your_base_or_null"
})

```

### Push notifications (Firebase approach)

To support PN on your side you should retrieve token for our senderID, send all needed data to us right after successful auth (you can call it in auth success block) and subscribe yourself to our topic.

``` javascript
import { Plugins } from '@capacitor/core';
const { AntViewerPlugin } = Plugins;

AntViewerPlugin.registerNotifications({ fcmToken: "put_your_FCM_token_there" })
.then((topic) => {
// Subscribe to topic
})
.catch(error => {
  console.log(error);
});
```

To open directly Feed screen from PN interaction handler just present it modally in right place.

``` javascript
import { Plugins } from '@capacitor/core';
const { AntViewerPlugin } = Plugins;

AntViewerPlugin.showFeedScreen();
```

### Add UI part

Antourage widget works as overlay over Capacitor web view. You can show and hide it whenever you want (navigation handlers or component lifecycle etc).

``` javascript
import { Plugins } from '@capacitor/core';
const { AntViewerPlugin } = Plugins;

AntViewerPlugin.showWidget();

AntViewerPlugin.hideWidget();

```

### Widget position

You can set any position from the list:
* topLeft
* midLeft
* bottomLeft

* topMid
* bottomMid

* topRight
* midRight
* bottomRight

Also you can set custom horizontal and vertical margin for each position. But some positions may ignore it. Max horizontal - 50, max vertical - 220.

``` javascript
import { Plugins } from '@capacitor/core';
const { AntViewerPlugin } = Plugins;

AntViewerPlugin.setPosition({ platform: "ios", position: "bottomLeft" }); // iOS only
AntViewerPlugin.setPosition({ platform: "android", position: "bottomLeft" }); // android only
AntViewerPlugin.setPosition({ position: "bottomLeft" }); // both

AntViewerPlugin.setMargins({platform: "ios", horizontal: 0, vertical: 30 }); // iOS only
AntViewerPlugin.setMargins({platform: "android", horizontal: 10, vertical: 50 }); // android only
AntViewerPlugin.setMargins({horizontal: 0, vertical: 30 }); // both

```

### Orientation (iOS only)

Your app may support only portrait orientation, but our widget should be able to use landscape orientation while playing video.
We suggest two approaches to solve it.

First of all you should enable ladnscape orientation in xcode project.
<img src="./screenshots/orientation.png" alt="Screenshots" width="100%" />

First approach:

You can use `cordova-plugin-screen-orientation` to be able to lock orientations occasionally depending on the content.

Just add two listeners to handle widget state:
``` javascript
import { Plugins } from '@capacitor/core';
const { AntViewerPlugin } = Plugins;

AntViewerPlugin.addListener('onViewerAppear', (info: any) => {
  console.log('viewer did appear');
  // window.screen.orientation.unlock();
});

AntViewerPlugin.addListener('onViewerDisappear', (info: any) => {
  console.log('viewer did disappear');
  //window.screen.orientation.lock('portrait');
});

```

Second approach (a bit easier):

I can lock main capacitor controller to portrait from plugin (but application will support lanscape). It means that your ionic UI that runs in webView will be in portrait only, but everthing outside capacitor controller (Antrourage screens, or some native modals etc) will be able to use landscape.

You just need to call this function after your app starts:
``` javascript
import { Plugins } from '@capacitor/core';
const { AntViewerPlugin } = Plugins;

AntViewerPlugin.lockCapacitorControllerToPortrait();
```

### Localization

By default android widget will use device's language: Swedish if it is chosen as device’s default language and English in other cases. But if you want to force app to use language that differs from device’s one - you can use method `setLocale(lang: String)`. Currently widget supports only English("en") and Swedish("sv").

``` javascript
import { Plugins } from '@capacitor/core';
const { AntViewerPlugin } = Plugins;

AntViewerPlugin.setLocale({ locale: "en" }); // or "sv"

```
 
## Author

Mykola Vaniurskyi, mv@leobit.com

## License

AntViewer is available under the MIT license. See the LICENSE file for more info.
