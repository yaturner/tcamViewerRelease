tCam Android Application
This repository contains the companion desktop application for the tCam cameras. It communicates with the cameras via a network connection using their json packet command set. It provides functionality to control the cameras, download and display data from them and analyze the radiometric data.

Get a current image.
Stream images from a connected camera at various rates.
Control remote picture and video recording and download images from the camera's local storage (tCam only).
Save and load radiometric image files.
Save and load radiometric video (stream) files.
Export radiometric data as a common format image file.
Graph temperature at up to five points from a stream or video file.
Update camera firmware (tCam-Mini requires FW 2.0 and beyond).
Discover cameras on the local network (requires tCam-Mini FW 3.0 and beyond)
The application is developed using the xojo development environment. 64-bit binary images are provided for Mac OS X, Windows and x86 Linux systems. A 32-bit binary image is provided for Raspbian or other ARM7HF Linux SBCs. Download the zip file for your platform. The application can be run directly from the unzipped directory by double clicking the application binary icon.

Note: Zip files for each application platform can be downloaded directly from my website as well if you don't want to clone this entire repository.

Version History
The latest version release notes are shown here. Please see the release_notes.pdf file for notes from previous versions.

Version 3.1.0

Support 63 character WiFi passwords with all tCam firmware and tCam-Mini firmware 3.1 and beyond
Disabled Graph when connected to a camera with a Lepton 3.0
Display “RAW” and “AGC” in color palette bar when connected to a camera with a Lepton 3.0
Worked around Xojo bug where pull-down menus didn't work properly in Linux builds (starting with version 3.0.0)
Platform Caveats
The Mac version should now be signed and is delivered as a Universal installer package. Let me know if you have any trouble.
You may need to make the Linux application file executable.
You may also have to authorize the application on the Windows platform since I don't yet package it for distribution in their online stores.
Windows users may need to install support for Bonjour (mDNS) using the bonjoursdksetup.exe installer from Apple found here.
Different Linux desktop systems render the toolbar differently and all toolbar items aren't visible since Linux renders the text next to the icon instead of beneath it. You can make the window wider to expose some important controls like Stream that has sub-menus or you can use the pull-down menus at the top of the window.
Linux users may need to install libwebkit2gtk to view the built-in documentation.
The Raspberry Pi versions basically require a Pi 4 to display a stream at the full rate. On slower Pi models the application may not be able to keep up and the controls may become unresponsive when streaming at the full ~9 FPS rate.
An advance apology - I develop on my Mac and do quick tests on Windows 7 and 10, and Ubuntu, Kubuntu and Raspbian. Although xojo provides pretty good cross-platform compatibility for OS X and Windows, sometimes there are issues with Linux. If you find some other issue, please let me know and I'll try to fix it.

Main Window
Main Window

Main window operation is described below.

Preferences
Preferences Window

The preferences window is used to configure the application. Preferences are stored on the computer and loaded each time the application starts.

Camera IP Address - Set the camera's IP address. Clicking the refresh button sets the computer's current network IP4 address with the lowest octet set to "1". If the camera is acting as an AP then this address will be the camera address "192.168.4.1". If the camera and computer are both connected to an external AP then replace the lowest octet with the address associated with the camera.
Discover - Displays the Camera Discovery window which is used to display the IP addresses of cameras on the same network (tCam-Mini cameras must be running FW 3.0 and beyond).
Manual Range - Allows setting a specific manual temperature range for the display of radiometric images.
Display Units - Allows setting the unit display used throughout the main window.
Stream Rate - Allows setting the requested stream rate from the camera when streaming is enabled (fastest possible rate down to one image every five minutes)
Update Camera Clock - Causes the application to set the camera's built-in clock to the current computer time on each connection. The clock is used to timestamp images.
Scale Display using Bilinear interpolation - Uses an algorithm that results in a slightly smoother image as it is increased from the camera's native 160x120 pixel resolution. De-selecting this uses a much faster algorithm that will work better on slower computers and when resizing the image at the cost of some smoothness.
Export Resolution - Sets the size of an exported image (160x120 pixels to 640x480 pixels) and specifies if only the image or the image plus additional information is rendered to the exported file.
Download Folder - Sets the default folder for downloaded/saved images.
Automatically check for updates - Selecting this enables the program to check for an updated version every time it is launched. It is always possible to check for an update using the Applications->Check for updates... menu item if this is de-elected. No information is transmitted during the check.
Connecting to an Ethernet Camera
The tCam-POE camera using its Ethernet interface has either a DHCP-served or statically assigned IPV4 address. This address is entered into the application preference's Camera IP Address field. A statically assigned address may be set using the Settings button as described below (Camera Settings Window).

Connecting to a WiFi Camera
The tCam cameras operate in one of two WiFi modes. By default they act as an Access Point (AP) and create their own WiFi network with the SSID "tCam-XXXX" or "tCam-Mini-XXXX" where XXXX are four hexadecimal digits. This makes it easy to connect to a camera right away. Once connected the camera may be reconfigured using the application to connect to an existing WiFi network, either getting a DHCP served IPV4 address from the network's router or with a statically assigned IPV4 address. This makes it possible for the computer running the application to talk to both the camera and the internet at large.

Connecting to a camera as Access Point
Configure the computer to connect to the camera's SSID. The camera always has a IPV4 address of "192.168.4.1" when it is acting as an Access Point so this number should be entered into the application preference's Camera IP Address field (this is the application's default value). Press the Connect button after configuring or verifying the preference IP address field.

Configuring the camera to connect to another WiFi network
Once connected the application can be used to reconfigure the camera to connect to an existing WiFi network using the Settings button as described below (Camera Settings Window). The camera may be configured to either get a DHCP served IPV4 address from the router or given a static IPV4 address on the network.

Connecting to a camera connected to another WiFi network
Connecting to a camera on an existing WiFi network requires the camera's IPV4 address to be entered into the application preference's Camera IP Address field before pressing Connect. For cameras running firmware prior to version 3.0, it may be necessary to log into the WiFi router or use a utility program (for example Fing on Android or nmap on Linux) to obtain the camera's IPV4 address if it has been assigned automatically using DHCP.

Discovering Cameras
tCam-Mini cameras running version 3.0 firmware or later, and all tCam and tCam-POE cameras implement mDNS (bonjour) for discovery. The Discover Cameras window displays all cameras on the local network. Selecting a camera and clicking Apply sets the Camera IP Address with the IP Address of the selected camera.

Discovery Window

Application Operation
The application is oriented around radiometric image files. It always displays the last image it processed. This may be a static image loaded from a file or taken by an attached camera. It may also be a series of images from a video file or streamed from the camera. Each image is displayed using a selected Palette to provide a false color image. The 16-bit radiometric data is linearly scaled to 8-bits and the selected palette used to generate 24-bit RGB pixel colors. When the camera is configured into AGC mode the 8-bit data from the camera is used directly with the selected palette.

Note that while the application is designed primarily for use with radiometric image files, it is also capable of displaying images taken when the camera's Lepton sensor has been configured into AGC mode. In this case, since the data from the camera no longer contains radiometric information, several functions (such as radiometric markers or histogram analysis) are not available.

Camera Controls
Camera controls are available when the application is connected to a camera. The main camera controls are displayed at the top of the main window. These controls and additional controls are displayed under the Camera pull-down menu.

Connect - Toggles the connection state with the camera. The connection state is shown in the Connection Status area. When first connected, and then periodically, the application requests the camera status and displays it in the Camera Status area.
Settings - Requests the current Lepton configuration and WiFi setup from the camera and displays the settings window.
Get - Get a single image from the camera.
Stream - Start (or Stop) the camera streaming images at the rate set in the Preferences Window. The stream may optionally be stored to a video file. Clicking the Stream button brings up a submenu.
Stream - Only display the stream.
Record - Select a video file to record the stream into and display the stream.
Stop - End a stream (close the video file if recording).
Snap - Take a picture and store it in the camera's local storage (tCam only). Equivalent to pressing the shutter button with the camera set to Image mode.
Record - Start or stop the camera recording a stream in its local storage (tCam only). Equivalent to pressing the shutter button with the camera set to Video mode.
Download - Download a selected set of image or video files from the camera's local storage (tCam only).
Power - Switch the camera off (tCam only).
Check for new Firmware - Checks to see if a newer version of the firmware for the connected camera is available to download from danjuliodesigns.com.
Update Firmware - Initiate a FW update process with cameras that can support it.
Camera Info - Display a pop-up (shown below) with information about the currently connected camera.
Camera Information Window

Camera Settings Window
The Camera Settings Window allows configuring the camera operation. Items with the associated "Update Camera" checkbox set will be updated in the camera if Apply is pressed.

Configuration Tab
Camera Configuration Window

Configuration items affect the Lepton's operation.

AGC Button - Selects between Radiometric operation or the Lepton's AGC mode which uses a built-in algorithm to improve visual image quality at the expense of outputting radiometric data. When AGC is selected the output data is 8-bits/pixel designed to be displayed through the color palette with improved visual characteristics and is useful to see differences in temperature in an image.
Gain Pulldown - Selects the Lepton's Gain mode. High gain is useful for images with similar temperatures. Low gain is useful for images with widely varying and high temperatures (for example when looking at fire). Automatic gain mode allows the Lepton to switch from High to Low gain as necessary based on the image.
Emissivity - Sets the Lepton's applied emissivity and is a value of 1-100%. Should be set based on the characteristics of the materials being imaged. Some useful materials are listed in the scroll-box. Selecting one of them automatically updates the emissivity value.
WiFi / Network Tab
Camera Network Window

The WiFi / Network tab configures the camera network interface.

Ethernet Interface
For cameras using an Ethernet interface (tCam-POE configured to use Ethernet) the tab displays Network items. Network items include the camera name and if a static IP should be set.

Camera Name - Configure the name of the camera as displayed in the Discover Cameras Window.
Camera Client Static Address - Selecting this checkbox and filling in the associated IPV4 address field allows configuring the camera with a static IPV4 address. The address must be on the same network and should not be in a range the network's router might assign automatically using DHCP. De-selecting the checkbox will enable the camera to request a DHCP served IPV4 address from the router.
Netmask - The netmask to use when using a static IPV4 address. Usually this will be "255.255.255.0".
WiFi Interface
For cameras using WiFi (tCam, tCam-Mini and tCam-POE configured to use WiFi) the tab displays WiFi items. WiFi items include whether the camera is acting as an Access Point (AP) or connecting to an AP (Client mode), the associated SSID and password and if a static IP should be set (in Client mode only - the camera always has the IP address of 192.168.4.1 in AP mode).

Camera is Access Point checkbox - Configure the camera's Wifi Mode as either Access Point (it creates a Wifi Network) or Client (it connects to another Wifi Network).
SSID - The Wifi Network SSID. This is the name of the WiFi Network the camera will create if it is in AP mode or the name of the WiFi Network it will attempt to connect too in Client mode. The maximum length is 32 characters.
Password - The Wifi Network WPA password. This is the password that is necessary to connect to the camera's WiFi Network if it is in AP mode or the password it will use to connect the another WiFi Network in Client mode. Leave the field blank if there is no password, otherwise the password must be between 8 - 32 characters long.
Camera Client Static Address - Selecting this checkbox and filling in the associated IPV4 address field allows configuring the camera with a static IPV4 address. This only applies to the camera when it is operating in Client mode. The address must be on the client network and should not be in a range the network's router might assign automatically using DHCP. De-selecting the checkbox will enable the camera to request a DHCP served IPV4 address from the router.
Netmask - The netmask to use when using a static IPV4 address. Usually this will be "255.255.255.0".
The application will be disconnected after changes to the Wifi / Network configuration are made. The application Camera IP Address field preference may need to be updated to reconnect.

Download Window
Selecting Download queries the connected camera for all files stored in its local storage. The files and their parent directories are displayed in the download window.

Download Window

The window allows selecting either entire folders for download or individual files within a folder for download to the destination parent folder. Click the associated Download checkbox next to either the folder name or file name and click Download to start downloading files. Selecting the Delete after download checkbox will delete the file or folder on the camera after it is downloaded.

Range/Palette Display
The Range/Palette display shows the currently selected palette with a marker showing the spotmeter temperature location within the range of temperatures. It also displays the minimum and maximum temperatures used to scale the image when the Lepton is operating in Radiometric output mode. These temperatures are simply the minimum and maximum temperature in the image's radiometric data when Auto Range Selection is enabled. They are the manual temperature range (set by the user in the Preferences window or automatically when the AR button is pressed) when Manual Range Selection is enabled.

Image Management
Image Management controls are available based on the type of operation occurring or image being displayed.

Browse - Allows opening a directory (Folder) of image and video files and displays forward and backward buttons in the Current Activity area.
Open - Allows opening a single image or video file.
Save - Allows saving the current image in a file.
Export - Allows saving the current image as a jpeg, png or tiff image, with or without additional metadata rendered to the image.
Graph - Allows graphing either a stream or video file. At least one of the spotmeter or four radiometric markers must be enabled to graph.
An example of a 320x240 pixel exported image (with metadata) is shown below.

Exported Image

Image Palette
A pull-down menu allowing selection between a set of false color maps. Different palettes are useful in visualizing various attributes of an image. For example the Rainbow HC palette, with its rapidly changing colors is good for showing temperature gradients while the Ironblack palette is good for emphasizing only the hotter areas in a scene.

Spot/Marker Temps
Displays the current enabled SpotMeter ("s") or Radiometric Marker temperatures ("m1" - "m4").

The SpotMeter temperature is taken from the telemetry data in the last image. It is based on a 4-pixel average.

The Radiometric Marker temperatures are computed based on the Radiometric data in the last image. They are also computed using a 4-pixel average.

Spotmeter Select
Clicking the Spotmeter Select button enables setting the spot meter position in the Lepton by clicking on a location in the image. Note that changing the spotmeter position causes a command to be sent to the camera setting the location. However the spotmeter display in the image and the temperature displayed above are not changed until a new image is loaded from the camera.

Radiometric Marker Selects
The Radiometric Markers are only enabled if the displayed image contains radiometric data (they are disabled if the image was generated by the Lepton while AGC is enabled).

Clicking on a Radiometric Marker Select button enables setting the associated marker position in the displayed image. The marker is displayed immediately since it is calculating the temperature at the location based on the existing image radiometric data.

Double clicking a Radiometric Marker Select button disables the marker if it is currently displayed.

Flat Field Correction
Clicking on the FFC button causes the connected camera to initiate a Lepton flat field correction.

Current Activity
The Current Activity area displays the source of the last loaded image and its timestamp. It also displays a pair of forward and backward buttons when browsing a folder.

Browse Controls

Video Playback
The Video Playback area displays controls and timestamp information when a video file has been opened. It also displays the frames-per-second of a playing video or stream.

A play/pause button, denoted by a single right-facing triangle, controls video playback. A position slider allows setting the video position.

Video files with a frame-rate of below 1 frame-per-second cause a second fast forward button, denoted by a double right-facing triangle, to appear. Pressing this button plays the video at a fixed rate of one frame-per-second instead of the video's normal rate (which could be as slow as one frame every five minutes!).

Video Fast Forward

Connection Status
Connection Status shows the current connection state, either Connected or Disconnected. While connected the application periodically sends a request for status. If the camera does not respond with a status response the application will assume the camera has been disconnected.

Camera Status
Information from the camera status responses are displayed in the Camera Status area including the camera name, and optionally battery level and charge status for tCam.

Auto/Manual Range Selection
The Auto/Manual Range Selection button toggles between Automatic and Manual Range modes when the Lepton is configured in Radiometric mode (the button is disabled if AGC is enabled).

In Automatic Range mode the minimum and maximum temperatures present in each image are used to linearly scale the radiometric data.

Manual Range mode uses a preset minimum and maximum temperature to scale the radiometric data. This mode is useful to eliminate radical image changes while streaming or playing back a video and the scene dynamic range changes from image to image resulting in very different false color mappings. Typically a manual range is set to be slightly greater than the largest expected scene range.

The Range mode can also be controlled via Preferences.

When the Auto/Manual Range Selection button is used to enter Manual mode, the minimum and maximum temperatures are set by rounding the existing scene minimum temperature down to next whole number value and the existing scene maximum temperature up to the next whole number value.

Lepton Configuration
Displays the Lepton's gain and emissivity settings for the current image.

The gain setting is either HIGH or LOW. When the camera's Lepton is allowed to automatically select the gain setting (via the Camera Settings) then it will use a High gain setting for scenes with a low dynamic range (-10°C to 140°C) for improved accuracy and resolution. It will switch to Low gain setting for scenes with a higher dynamic range.

The emissivity setting is a percent, from 1-100, that the Lepton uses to improve accuracy when computing the radiometric temperature of each pixel. It should be set to match the emissivity of objects in the scene.

Histogram Analysis
The Histogram Analysis area displays a histogram showing the relative number of pixels for each of the 256 values (bins) that result from the linear transformation of the radiometric data or are direct from the camera when AGC is enabled.

A pair of markers can be dragged onto the histogram. The markers display the temperature of the bin they are over when the image contains radiometric data.

Additional information is displayed about the region between the two markers when both are dragged onto the display.

Population - Percent (and number) of pixels out of the Lepton's 19200 total pixels between the markers.
@minP (radiometric data only) - The temperature of the bin with the least number of pixels in the region between the two markers.
@maxP (radiometric data only) - The temperature of the bin with the highest number of pixels in the region between the two markers.
Mean (radiometric data only) - The mean temperature in the region between the two markers.
Average (radiometric data only) - The average temperature in the region between the two markers.
