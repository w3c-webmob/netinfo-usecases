#Use case and requirements for network information
This document outlines the use cases and requirements for giving web applications access to network information. The use cases and requirements were gathered by looking at what both Websites and native platforms currently do with such information.

The main questions this document seeks to explore are:

 * What can an application do when it knows the kind of connection the user's device is using?
 * How does an application respond to when the device switches from one kind of network connection to another?
 * What are the motivations for using this information within an application?
 * Does the application use raw bandwidth info to adapt content?

##Web

### BBC News Website
When the user tries to watch a video on cellular, the Website warns the user that it might cost them money if they proceed.

![image](images/bbc_cellular.png)

When the site is accessed over WIFI, the warning is not presented to users. Note that this is distinctly different from adaptive video streaming, which needs to happen both over WIFI and cellular.

### WebRTC Web App
A developer is dealing with a WebRTC powered web application where users can communicate using audio & video streams as well as data channels, and they were trying to find a way to adapt the best user media constraints matching the capacity of the user's connection (e.g. to avoid them to receive a full HD stream if their connection wouldn't be capable of handling it). The developer started looking at navigator.connection.bandwidth; though it may be probably the responsibility of WebRTC to adapt automatically (work is continuing here). 

Many thanks to @n1k0 for this use case. 

### [OPEC Portal](http://portal.marineopec.eu/v3/static/index.html)
The developer wishes to send different data (geographic, 3D marine data taken by satellites) from a central server to users. Currently it sends everything but the developer is working on a new solution to only send what is needed. Bandwidth is an important consideration, which may or may not help with defining what to send. One example could be allowing animation of a year's worth of data, if the user is on a very fast connection. If they are not, it would be far to much data to download. 

Many thanks to Shane Hudson for this use case. 

### Performance KPIs
Some enterprise applications will have key perfomance indicators or standard goals set to make sure a page loads under 2 seconds (for example). Specific enhanacements are becoming difficult to adhere to as bandwidth is unpredictable for different users. Being able to determine the bandwidth would allow developers to serve complicated and rich apps to users with higher bandwidth, and more restricted or performance-enhanced sites to those with lower, meaning targets and met and users stay happy!

Adapted from Anon's comments on OkSoClap (many thanks!).

### Streaming Game Application 
The game deverlopers tried to detect bandwidth in JavaScript before loading the actual streaming plugin. The thought process was that they would try to prevent people with slow connections from having to download a 3MB Java applet or large Flash client and then still being unable to load the game. This was probably an inversion of priorities, but they did it anyway. They tried two methods: the first was to make XMLHttpRequests for increasingly large files, and seeing which one failed before the end of the timeout. This was obviously a bad idea since it introduces latency and TCP connection time. The second approach was basically the same, but instead of downloading several files, we downloaded one big file over CORS and tracked its progress in JavaScript over time, finding an average after n seconds. This way we had a slightly more accurate metric, but it still wasn't great. 

Thank-you to Anon for this use case!

### Music Web Application 
Also provides streaming radio. The developers noticed that users are continually streaming music via MP3 streams or RTMP and have the need to understand on the client side the available bandwidth. They have run some tests with sample downloaded elements with known size but highly variable results. They concluded being able to switch to lower bandwidth streams would be quite valuable. Additionally ability to have this on mobile web pages would enable making decisions about audio quality tuned to mobile bandwidth limitations.

Many thanks to @artlung for this use case!

### Retina Images
The developer is using some custom bandwidth detection to only serve retina images when there's enough bandwidth available. 

Many thanks to @rowno1 for this use case!

##iOS
IOS can tell a user that a system update is available, but does not allow them to download the update unless they are connected to WIFI. iOS will also pause system updates if the user loses the connection to a WIFI network and automatically resumes downloads once the user connects to WIFI.

![image](images/ios_needs_wifi.png)

Note that the buttons in the image are disabled - the download button serves both as a button and status indicator.

### Dropbox
The Dropbox application allows users to select whether videos shot on the device should be automatically uploaded using cellular data.

![Menu that controls Dropbox's camera uploads](images/dropbox_camera_sync.png)

### Spotify
The Spotify application allows users to select whether synchronization of audio tracks between devices can occur over cellular.

[Spotify sync menu](images/spotify_sync_menu.png)

### Rdio
The Rdio application allows users to control both the quality of audio and synchronization over either WIFI or cellular. The options available are "alway" (cellular or WIFI), "Wi-Fi only", or "never".

![Rdio's settings menu](images/rdio_settings.png)

### AppStore Application
The AppStore does not allow users to download applications over 100Mbs unless they are on WIFI.

![image](images/appstore_cell_limit.png)

Although the store will allow the user to purchase an application, it will queue the application for download for when the user next connects to WIFI.

If the user transitions from WIFI to cellular in the middle of a large download, iOS stops the download and warns the user.


![image](images/ios_cell_switch.png)

### Audible
Audio books are generally around 50-100mb and come in individual pieces (which contain a range of book chapters). This means that a book can be on average about 100mb.

The Audible application on iOS won't let a user download books over cellular unless they explicitly set an option in the application's setting.

![image](images/audible_wifi_only.png)

Even when set to allow downloading over the cellular network, audible lets the user know that they can disable this through the settings.

![image](images/audible_over_cell.png)

The Audile app will also detect when network connection switches from WI-FI to celular and inform the user. When this happens, Audible will either continue the download on celular automatically or halt the download.

![image](images/audible_cell_switch.png)

Downloading large audio books takes significant time depending on bandwidth. It is often the case that a book is not fully downloaded before a user wants to listen (e.g., the user starts a download over WIFI, but then leaves their house or closes the application).

![image](images/audible_error.png)

 In such cases, it is possible to resume a download over cellular - but only if the user has explicitly allowed this in the application's settings. Note that this is controlled by the application, and not at the OS level. If the user has not allowed downloading over cellular, they get the option to enable this.

![image](images/audible_wifi_warn.png)

### Tweetbot
Tweetbot and several other Twitter apps support [streaming](https://dev.twitter.com/docs/streaming-apis), but only make use of it on WiFi networks.

![](images/tweetbot_wifi.png)

On cellular connections, you have to manually pull down to fetch new data and update the view.

![](images/tweetbot_3g_step_1.png)
![](images/tweetbot_3g_step_2.png)
![](images/tweetbot_3g_step_3.png)

### Native iOS messages app (failed use case)
If there's a data connection, then the Native iOS messages app uses iMessage to send the text message (rather than SMS), but over GPRS it usually always fails, and thus message isn't sent. If this was done using web, we'd have the same problem: "is there a data connection? Great - send some data" - but this fails because the reception is crap. I've always wondered if we acctually need a ping api to give us latency to a resource - then we can decide whether to proceed (in executing a data exchange). 

Many thanks to @rem for this use case.

## Android

## Windows Phone

## Discussion

From the apps we've looked at, the main cases appear to be:

* Warn the user that doing something over cellular could cost them money.
* Give the user control as to whether large uploads/downloads should happen over cellular (mostly related to synchronizing media data like photos, videos, and audio files).
* Prevent accidental data transfer over cellular, which could use up the user's data transfer quota and/or cost them money. 

## Requirements
In order to be able to replicate the functionality seen in native applications, the web platform needs to:

 * provide access to the connection type the system is using to receive data: namely cellular, WIFI, or none (e.g., airplane mode). This information needs to be available either immediately on page load or as close as possible to it. If the connection type changes, then the change needs to be reflected in the API in a way that script can access the updated information.

 * provide a means for scripts to be notified if the connection type changes. This is to allow developers to make dynamic changes to the DOM and/or inform the user that network connection type has changed.

## Acknowledgments
Huge thanks to Yoav Weiss, Mathias Bynens, Tobie Langel, and Michael Hung fo.
