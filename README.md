#Use case and requirements for network information
This document outlines the use cases and requirements for giving web applications access to network information. The use cases and requirements were gathered by looking at what both Websites and native platforms currently do with such information. 

##Web
This section describ

### BBC News Website
When the user tries to watch a video on cellular, the Website warns the user that it might cost them money if they proceed. 

When the site is accessed over WIFI, the warning is not presented to users. Note that this is distinctly different from adaptive video streaming, which needs to happen both over WIFI and cellular.

##iOS
IOS can tell a user that a system update is available, but does not allow them to download the update unless they are connected to WIFI. iOS will also pause system updates if the user loses the connection to a WIFI network and automatically resumes downloads once the user connects to WIFI. 

### AppStore Application
The AppStore does not allow users to download apps over 100Mbs unless they are on WIFI. 

Although the store will allow the user to purchase an application, it will queue the application for download for when the user next connects to WIFI. 

If the user transitions from WIFI to cellular in the middle of a large download, iOS stops the download and warns the user.

### Audible 
The Audible app on iOS won't let a user download books over celular unless they explicitly set an option in the application's setting. Books are generally around 50-100mb and come in idividual pieces (which contain a range of book chapters). This means that a book can be on average about 100mb.  

The Audile app will also detect when network connection switches from WI-FI to celular and warn the user. When this happens, Audible will either continue the download on celular or halt the download. The user can configure this behavior in the application's settings. 

As downloading large audio books takes significant time depending on bandwidth. It is often the case that a book is not fully downloaded before a user wants to listen (e.g., the user starts a download over WIFI, but then leaves their house or closes the application). In such cases, it is possible to resume a download over celular - but only if the user has explicitly allowed this in the application's settings. Note that this is controlled by the application, and not at the OS level.  

## Android

## Windows Phone
