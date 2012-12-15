Sencha Cordova Builder
======================

Enables the automatic creation, building, and running of PhoneGap (Cordova) projects with Sencha Touch. Since the project
is just a collection of build files, all that's needed is to import a file in your Sencha Touch build.xml and implement
your logic where you want.

This current release was developed and tested on a Mac. It should work just as well on a PC but testing has not
been done yet.

This project has absolutely no affiliation with Sencha or PhoneGap.

Released under the MIT license. See LICENSE.md for details.

Goals
-----

- Simple installation and configuration
- Keep it familiar, no extra tools/scripts required
- Work with the framework, not against it
- Use conventions already provided by Sencha Touch

Requirements
-----------

Assuming you want to develop for both Android and iOS:

- Android SDK
- Mac
- xCode
- PhoneGap (Cordova) 2.2+
- Sencha Touch 2.1+
- Sencha Cmd 3.0+

Installation
------------

1. Download and extract the project
2. Modify the `cordova.properties` file to match your environment. At a minimum you'll need to modify the `cordova.lib` property which is the path to your PhoneGap framework. Unless you're using PhoneGap 2.2, you might also need to modify the `cordova.android.tools.js` and `cordova.ios.tools.js` as these point to the PhoneGap javascript libraries for their respective platforms.
3. Finally, import the main cordova build file into your Sencha Touch build.xml file then implement the build you want to run. Assuming the project is extracted to the root directory and you're building for Android:

        <import file="/sencha-cordova-builder/build-cordova.xml" />
        <target name="-after-build" depends="-build-android" />

Usage
-----

### Building for Android

To build for Android, plug into the `-after-build` target provided by Sencha Touch as follows:

    <target name="-after-build" depends="-build-android" />

The Sencha Cordova Builder provides various steps for you to inject your own logic during some key phases in the build process.

- -before-init-android
- -after-init-android
- -before-build-android
- -after-build-android

A common scenario might be to tap into the `-after-build-android` phase to automatically clean/compile/run your Android project. Assuming you're on a mac, here are some examples:

    <target name="-after-build-android">
        <!-- clean -->
        <exec executable="${cordova.android.project}/cordova/clean" />

        <!-- compile -->
        <exec executable="${cordova.android.project}/cordova/debug" />

        <!-- emulate -->
        <exec executable="${cordova.android.project}/cordova/emulate" />

        <!-- or all in one shot (clean, compile, emulate) -->
        <exec executable="${cordova.android.project}/cordova/BOOM" />
    </target>
    
If you want to rebuild the Android project, you'll need to delete the `_android.built` file that was placed in the root
of your Sencha Touch app. This file is used as a flag to know when the build process has completed. 

### Building for iOS

To build for iOS, plug into the `-after-build` target provided by Sencha Touch as follows:

    <target name="-after-build" depends="-build-ios" />

The Sencha Cordova Builder provides various steps for you to inject your own logic during some key phases in the build process.

- -before-init-ios
- -after-init-ios
- -before-build-ios
- -after-build-ios

If you want to rebuild the Android project, you'll need to delete the `_ios.built` file that was placed in the root
of your Sencha Touch app. This file is used as a flag to know when the build process has completed. 

### Building Android and iOS Together

As a convenience, you can build Android and iOS together by plugging into the `-after-build` target provided by Sencha Touch as follows:

    <target name="-after-build" depends="-build-cordova-all" />

You can of course still tap into the following phases:

- -before-init-android
- -after-init-android
- -before-build-android
- -after-build-android
- -before-init-ios
- -after-init-ios
- -before-build-ios
- -after-build-ios

If you want to rebuild the Android project, you'll need to delete the `_android.built` and `_ios.built` files that were placed in the root
of your Sencha Touch app. These files are used as flags to know when the build process has completed. 








