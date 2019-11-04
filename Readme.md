SETUP ANDROID STUDIO FOR REACT NATIVE WINDOWS 7
https://facebook.github.io/react-native/docs/getting-started
or watch
https://www.youtube.com/watch?v=YVaGbwQephg
https://www.youtube.com/watch?v=uhuoTcbquic

https://www.ryadel.com/en/react-native-visual-studio-code-windows-hello-world-sample-app/

1. search for system, click advanced system settings, advance tab, click
   environment variables, user variables list click new
   new user variable name = ANDROID_HOME
   new user variable value = c:\Users\YOUR_USERNAME\AppData\Local\Android\Sdk
   new user variable name = JAVA_HOME
   new user variable value = C:\Program Files\Java\jdk1.8.0_231

2. EDIT User PATH variables list then click EDIT
   put semicolon in the end of the line and paste
   C:\Users\mathew_uy\AppData\Local\Android\Sdk\platform-tools
   ;
   C:\Users\mathew_uy\AppData\Local\Android\Sdk\tools\bin
   ;
   C:\Program Files\Java\jdk1.8.0_231\bin
   ;
   C:\Users\mathew_uy\AppData\Local\Android\Sdk\emulator\emulator
   ;
   C:\Users\mathew_uy\AppData\Local\Android\Sdk\tools

3. System variables list higlight PATH then click EDIT
   put semicolon in the end of the line and paste
   c:\Users\YOUR_USERNAME\AppData\Local\Android\Sdk\platform-tools
   important: DO NOT OVERRIDE EXISTING VARIABLES.

4. Install Java SE Development Kit 8u231 https://www.oracle.com/technetwork/java/javase/downloads/jdk8-downloads-2133151.html check windows compatibility

5. Next, select the "SDK Tools" tab and check the box next to "Show Package Details" here as well. Look for and expand the "Android SDK Build-Tools" entry, then make sure that 28.0.3 is selected.

C:\Users\mathew_uy\AndroidStudioProjects\MyApplication (main app)
open cmd...
cd %ANDROID_HOME%/tools
emulator -list-avds
emulator -avd Pixel_XL_API_28

install npm install -g react-native-cli

1. react-native init "name of app"
2. react-native run-ios || react-native run-android

Set-ExecutionPolicy Default

https://www.youtube.com/watch?v=8FEm1SjL1Vg

1.create directory android/app/src/main/assets

2. run following command from project root directory

react-native bundle --platform android --dev false --entry-file index.js --bundle-output android/app/src/main/assets/index.android.bundle --assets-dest android/app/src/main/res

3. run again the command : react-native run-android

The solution this problem is edit file the project node_modules\metro-config\src\defaults\blacklist.js

Replace :

var sharedBlacklist = [
/node*modules[/\\]react[/\\]dist[/\\].*/,
/website\/node*modules\/.*/,
/heapCapture\/bundle\.js/,
/._\/**tests**\/._/
];

with :

var sharedBlacklist = [
/node*modules[\/\\]react[\/\\]dist[\/\\].*/,
/website\/node*modules\/.*/,
/heapCapture\/bundle\.js/,
/._\/**tests**\/._/
];
then run
react-native bundle --platform android --dev false --entry-file index.js --bundle-output android/app/src/main/assets/index.android.bundle --assets-dest android/app/src/main/res

IMPORTANT: if build fails after installation run
cd android && gradlew clean
then run react-native run-android

Packages installed:

1. npm install --save react-native-image-picker
   react-native link react-native-image-picker

a. change in /ios/NameOfApp/plist
<dict>
...
<key>NSAppTransportSecurity</key>
<key>NSPhotoLibraryUsageDescription</key>
<string>$(PRODUCT_NAME) would like access to your photo gallery</string>
    <key>NSCameraUsageDescription</key>
    <string>$(PRODUCT_NAME) would like to use your camera</string>
<key>NSPhotoLibraryAddUsageDescription</key>
<string>$(PRODUCT_NAME) would like to save photos to your photo gallery</string>
    <key>NSMicrophoneUsageDescription</key>
    <string>$(PRODUCT_NAME) would like to use your microphone (for videos)</string>
</dict>

b. change in /android/AndroidManifest.xml
<uses-permission android:name="android.permission.CAMERA" />
<uses-permission android:name="android.permission.WRITE_EXTERNAL_STORAGE" />
