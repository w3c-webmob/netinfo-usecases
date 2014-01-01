#Use case and requirements for network information
This document outlines the use cases and requirements for giving web applications access to network information. The use cases and requirements were gathered by looking at what both Websites and native platforms currently do with such information.

The main questions this document seeks to explore are:

 * What can an application do when it knows the kind of connection the user's device is using?
 * How does an application respond to when the device switches from one kind of network connection to another?
 * What are the motivations for using this information within an application?
 * Does the application use raw bandwidth info to adapt content?

##Web
The following are examples of web applications that use various means to detect if a user is on Wi-Fi or cellular. 

### BBC News Website
When the user tries to watch a video on cellular, [BBC News](http://bbc.com/news/) warns the user that it might cost them money if they proceed.

![BBC News Website warns users of potential costs to watching videos online](images/web_bbc_cellular.png)

When the site is accessed over Wi-Fi, the warning is not presented to users. Note that this is distinctly different from adaptive video streaming, which needs to happen both over Wi-Fi and cellular.

According to Jim Lay of the BBC:

> It's part of our GeoIP service to detect mobile gateways, which is then used - we show it on all devices tethered laptops as well as mobile ones, and the single shown on load message is okay for this - doesn't matter if the user is flip-flopping across a mobile and non-mobile connection during a session.
>
> It's possible that knowing during a page session that it's swapped between would be useful, as well as using it for the message we also use it for selecting appropriate quality media.


##iOS
This section examines iOS 6 and 7, as well as various applications. 

### Settings 
Through iOS's settings application, iOS provides users with the ability to control which applications can communicate over cellular. In addition, the menu shows how much data each application has transferred over cellular. 

![iOS cellular menu](images/ios_cellular_settings.png)

iOS can tell a user that a system update is available, but does not allow them to download the update unless they are connected to Wi-Fi. iOS will also pause system updates if the user loses the connection to a Wi-Fi network and automatically resumes downloads once the user connects to Wi-Fi.

![iOS update screen: tells the user that Wi-Fi is required to perform the update to iOS7](images/ios_needs_wifi.jpg)

Note that the buttons in the image are disabled - the download button serves both as a button and status indicator.

### Camera and photos 
Through the settings provided by iOS's camera application, users have the ability to control if their photos are uploaded to Apple's [iCloud service](https://www.icloud.com/) when the device is connected to Wi-Fi.

![Camera and photos settings menus](images/ios_camera.png)

### Dropbox
The [Dropbox](https://itunes.apple.com/en/app/dropbox/id327630330) application allows users to select whether videos shot on the device should be automatically uploaded using cellular data.

![Menu that controls Dropbox's camera uploads](images/ios_dropbox.png)

### Spotify
The [Spotify](https://itunes.apple.com/en/app/spotify/id324684580) application allows users to select whether synchronization of audio tracks between devices can occur over cellular.

![Spotify sync menu](images/ios_spotify_sync_menu.png)

### Rdio
The [Rdio](https://itunes.apple.com/us/app/rdio/id335060889) application allows users to control both the quality of audio and synchronization over either Wi-Fi or cellular. The options available are "alway" (cellular or Wi-Fi), "Wi-Fi only", or "never".

![Rdio's settings menu](images/ios_rdio_settings.png)

### AppStore Application
The AppStore does not allow users to download applications over 100Mbs unless they are on Wi-Fi.

![A pop-up in iOS warns the user if an application exceeds 100Mb](images/ios_appstore_cell_limit.jpg)

Although the store will allow the user to purchase an application, it will queue the application for download for when the user next connects to Wi-Fi.

If the user transitions from Wi-Fi to cellular in the middle of a large download, iOS stops the download and warns the user.

![iOS will detect when the device switches from Wi-Fi to cellular and stops downloads that exceed 100Mb](images/ios_cell_switch.png)

### Audible
Audio books are generally around 50-100mb and come in individual pieces (which contain a range of book chapters). This means that a book can be on average about 100mb.

The [Audible](https://itunes.apple.com/us/app/audiobooks-from-audible/id379693831?mt=8) application on iOS won't let a user download books over cellular unless they explicitly set an option in the application's setting.

![Audible's app settings on iOS](images/ios_audible_wifi_only.png)

Even when set to allow downloading over the cellular network, audible lets the user know that they can disable this through the settings.

![Audible pops up a warning to let the user know they are about to download a large file over cellular](images/ios_audible_over_cell.png)

The Audile app will also detect when network connection switches from WI-FI to cellular and inform the user. When this happens, Audible will either continue the download on cellular automatically or halt the download.

![During a download, Audible informs the user if it detects that the connection to Wi-Fi is lost.](images/ios_audible_cell_switch.png)

Downloading large audio books takes significant time depending on bandwidth. It is often the case that a book is not fully downloaded before a user wants to listen (e.g., the user starts a download over Wi-Fi, but then leaves their house or closes the application).

![An audio book that has failed to completely download in the Audible application](images/ios_audible_error.png)

 In such cases, it is possible to resume a download over cellular - but only if the user has explicitly allowed this in the application's settings. Note that this is controlled by the application, and not at the OS level. If the user has not allowed downloading over cellular, they get the option to enable this.

![Audible warns the user that they are not connected to Wi-Fi, and explicitly prevents a download from happening.](images/ios_audible_wifi_warn.png)

### Facebook
[Facebook](https://itunes.apple.com/en/app/facebook/id284882215?mt=8) application on iOS allows to control if videos should autoplay (or not) on cellular.

![Facebook's settings on iOS](images/ios_facebook.png)

### Tweetbot
The [Tweetbot](http://tapbots.com/software/tweetbot/) application supports [streaming](https://dev.twitter.com/docs/streaming-apis), but only make use of it on Wi-Fi networks.

![Tweetbot streaming over Wi-Fi](images/ios_tweetbot_wifi.png)

On cellular connections, the user has to manually pull-down to fetch new data and update the view.

![Tweetbot requiring user action in order to refresh](images/ios_tweetbot_3g_step_1.png)

User pulls down: 

![User performing a "pull down" action](images/ios_tweetbot_3g_step_2.png)

Any new content is loaded: 

![Tweetbot loads content from the Web](images/ios_tweetbot_3g_step_3.png)

### iOS Messages application
If there's a data connection, then the Native iOS [messages application](https://www.apple.com/ios/messages/) uses the [iMessage cloud service](http://en.wikipedia.org/wiki/IMessage) to send the text message (rather than SMS), but over GPRS it usually always fails, and thus message isn't sent.

### Google Maps
[Google Maps](https://itunes.apple.com/en/app/google-maps/id585027354?mt=8) recommends turning on Wi-Fi to improve location accuracy. Users will generally see this message when the application is launched.

![Pop-up on Google Maps on iOS, asking users to enable wifi to improve accuracy](images/ios_google_maps.png)

### ABC iview
The Australian Broadcasting Corporation's (ABC) [iview application on iOS](https://itunes.apple.com/au/app/abc-iview/id401778175) does not provide any settings for controlling which connection type should be used when consuming content. Instead, if the application detects a cellular connection, it pauses the download of content and displays a confirmation dialog that warns the user: "3G in use, charges may apply".

![iview's confirmation dialog](images/ios_iview.png)

## Android
The following is a sample of Android applications running on mobile devices running Android 4.x.  

### Updates on Android
Android affords users the choice to select that applications should only be updated over Wi-Fi. It also allows updating at "any time" (meaning over cellular), but warns users that they may incur charges.

![Android's settings for managing how applications should be updated](images/android_google_play.png)

## Economist
The Economist application provides users with options for controlling which connection type is used to download new issues of the magazine. 

![The Economist app's settings for managing what content is downloaded over which connection](images/android_economist.png)

In this case, new issues of the magazine will be auto-downloaded over cellular or Wi-Fi. Note that these options are unlike other applications in this sample, in that it explicitly lists "3G" instead of "cellular" or Wi-Fi. It is unclear if "3G" literally means a "3G" connection or if downloads will occur on other cellular connection types, such as GPRS or on more modern connection types the phone supports (e.g., "4G"). 

It must be noted that this option also appears on devices that don't support cellular connections (e.g., the Nexus 7 tablet). Showing the user options to synchronize items over a connection type that is not supported by the device can obviously be confusing.

### Google Play Store
[Google Play Store](https://play.google.com/store?hl=en) offers an option to download app updates only via Wi-Fi.

![Android's options for which connections can be used for auto-updating applications](images/android_google_play.png)

It also has settings to enable a warning before streaming over a mobile network and a setting to choose the preferred network for movie downloads.

![On Android, users can enable a setting that will warn them if they attempt to stream media over a mobile network](images/android_google_play_warning.png)

![Android allows the user to select which connection type to use for downloads](images/android_google_play_download_network.png)

### Google Play Music
[Google Play Music](https://play.google.com/store/apps/details?id=com.google.android.music&hl=en) allows the user to automatically cache and/or download the music only while on Wi-Fi. It also offers the settings to adjust the quality of the music stream and to forbid it while on a mobile connection.

![Settings for Google Play Music](images/android_play_music.png)

### Netflix 
Netflix affords users the choice to restrict video playback to Wi-Fi only.

![Netflix's app settings on Android](images/android_netflix.png)

### Facebook
Just as with iOS, Facebook gives the user the choice to only auto-play videos when connected to Wi-Fi. 

![Facebook's app settings on Android](images/android_facebook.png)

### Evernote
The Evernote application affords users the choice to only do synching when connected to a Wi-Fi network. 

![Evernote's syncing options on Android](images/android_evernote.png)

### Pocket
The Pocket application gives users control as to whether downloads should occur exclusively over Wi-Fi. 

![Pocket's application settings on Android](images/android_pocket.png)

### YouTube
The [YouTube](https://play.google.com/store/apps/details?id=com.google.android.youtube&hl=en) application on Android offers the possibility of prefetching videos in advance while on Wi-Fi and charging.
>>>>>>> Added links, cleanup text, typos, alt text

![YouTube settings on Android](images/android_youtube.png)

### Spotify
Same as for iOS, [Spotify](https://play.google.com/store/apps/details?id=com.spotify.mobile.android.ui) on Android has a setting to allow downloads over the mobile network.

![Spotify's settings on Android](images/android_spotify.png)

### Gmail and Mail
[Gmail for Android](https://play.google.com/store/apps/details?id=com.google.android.gm&hl=en) offers a setting to download attachments only via Wi-Fi.

![Android Gmail](images/android_gmail.png)

The same option appears in Android's mail program. 

![Android mail](images/android_mail.png)

## Windows Phone
Windows Phone provides users with the option to allow mobile data to be used in the event of limited Wi-Fi connectivity. When this option is changed to "use mobile data", the phone informs that user that "your phone will use mobile data when Wi-Fi connectivity is limited. This will use your data plan and may incur charged". It's unclear what "connectivity is limited" means.

![Windows Phone 8 - Mobile network setting](images/wp_limited_wifi.png)

In addition, Windows Phone 8 includes a "data sense" feature that claims to "find more efficient ways to use mobile data and display your usage. For example, some data will download only when you are connected to Wi-Fi". The feature allows the user to set a download limit for cellular connections and will notify the user when that limit is exceeded. 

![Windows Phone 8 - Data sense feature](images/wp_datasense.png)

### Photos and videos
Windows phone 8 allows users to control whether photos are synchronized over Wi-Fi and/or cellular. Window Phones 8 restricts what can be sent over which connection type. For example, "good quality" photos can be sent over cellular, but "best quality" photos can only be send over Wi-Fi. Videos, irrespective of quality, can only be synchronized over Wi-Fi or not at all. 

![Windows Phone 8 - Photos and videos application setting](images/wp_photos.png)

## Discussion

From the apps we've looked at, the main cases appear to be:

* Warn the user that doing something over cellular could cost them money.
* Give the user control as to whether large uploads/downloads should happen over cellular (mostly related to synchronizing media data like photos, videos, and audio files).
* Prevent accidental data transfer over cellular, which could use up the user's data transfer quota and/or cost them money. 
* Advise the user to activate Wi-Fi to improve location accuracy.

## Requirements
In order to be able to replicate the functionality seen in native applications, the web platform needs to:

 * provide access to the connection type the system is using to receive data: namely cellular, Wi-Fi, or none (e.g., airplane mode). This information needs to be available either immediately on page load or as close as possible to it. If the connection type changes, then the change needs to be reflected in the API in a way that script can access the updated information.

 * provide a means for scripts to be notified if the connection type changes. This is to allow developers to make dynamic changes to the DOM and/or inform the user that network connection type has changed.

## License
![CC0](http://i.creativecommons.org/p/zero/1.0/80x15.png) To the extent possible under law, the [contributors](https://github.com/w3c-webmob/netinfo/graphs/contributors) have waived all copyright and related or neighboring rights to this work. In addition, as of 21 December 2013, the editors have made this document available under the Open Web Foundation Agreement Version 1.0, which is available at http://www.openwebfoundation.org/legal/the-owf-1-0-agreements/owfa-1-0. 

Parts of this work may be from an existing document. If so, those parts are instead covered by the license of the existing document document.

Screenshots used in this work are from copyrighted software applications. Their use in this document fall under [fair use](http://en.wikipedia.org/wiki/Fair_use).

## Acknowledgments
See the [list of contributors on GitHub](https://github.com/w3c-webmob/netinfo/graphs/contributors) to see who authored this document. 

Huge thanks to Yoav Weiss, Mathias Bynens, Tobie Langel, Michael Hung fo, Jim Ley, Fernando Jiménez Moreno, Nicolas Perriault, Joe Crawford, Shane Hudson, Roland Warmerdam, Remy Sharp, and Andrew Overholt.
