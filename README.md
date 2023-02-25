## tCam Android Application
This repository contains an APK version of the tCamViewer Android Application.  This app is designed to work with danjuliodesigns, LLC [tCam family](https://github.com/danjulio/tCam) cameras.

### Release Notes
This is an alpha release, designed for early testing. It may have bugs and you are encouraged to use the github issues tracker to log them.  

Streaming is broken in this release. It works but only in fits-and-spurts.  It's gonna be fixed :-)

### Installation
The app APK file has to be installed into your Android phone by opening it.  You may get a warning since you are doing this outside of the Play Store official installation process. To get around this warning you must enable "Install unknown apps" in Advanced Settings for the browser you use to download the APK. Usually the browser will prompt you to go to this setting after you download the APK file and attempt to open it.  Note that this is a security hole and you should probably disable this setting after installing the app.

### Operation
The app has three screens.

#### Camera Screen

![App Camera Screen](pics/app_camera_screen.png)

The Camera Screen is used to view and save images from the camera. 

1. CONNECT/DISCONNECT - Manage connection to a camera (a valid IP address must be configured first).
2. GET - Get an image from the camera and display it.
3. STREAM - Start or stop streaming.
4. Pallete - Select the palette to use when colorizing the image.  The palette may also be changed by touching the top or bottom of the palette bar.
5. SAVE - Save the current image to the library in tjsn format.

Touching the image will set the spot meter to that location.  The spot meter will be updated on the image when the next image is obtained (via GET or when streaming).

#### Settings Screen

![App Settings Screen](pics/app_settings_screen.png)

The Settings Screen is used to configure both the camera and the app.  Note that the CAMERA SETTINGS section is only displayed when the app is connected to a camera.  Clicking SAVE will update the camera and app.  Clicking CANCEL will throw away any changes.

#### Library Screen

![App Library Screen](pics/app_library_screen.png)

The Library Screen displays saved tjsn files.  Click on an image to select it for browsing or deletion.  Click the Playback button to browse selected images.  Click the Trashcan icon to delete them.

#### Browse Screen

![App Browse Screen](pics/app_browse_screen.png)

Swipe left or right to move between selected images.  Touch the top or bottom of the palette bar to change palettes.  Click the Sharing button to export jpeg versions of the image to the phone's photo library.  Click the Trashcan to delete the image.