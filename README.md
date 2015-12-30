# Android Source Swap

NodeJS program to easily switch the Android SDK Sources which Android Studio attaches when debugging.

## Reason 
When running an Android application on a device with a different Android SDK Version that the _compileSdkVersion_ used in _build.gradle_, debugging in Android Studio may result in off-sync lines. E.g. build an app againt Android SDK 23 and run it on a phone with Kitkat (Android 4.4, SDK API Version 19). Whil stepping through Android system classes, the files are not in sync.

A (stackoverflow answer)[http://stackoverflow.com/a/32252259/2225619] suggested renaming the Android Source folders for the time of debugging, as other solutions like changing the _compileSdkVersion_ especially when using support libraries results in numerous compilation errors.

## Installation
Either globally install the npm module using
````
npm install -g android-source-swap
````

or download the _swap-source.js_ file and place it in your Android project root folder or a script folder. Execute with
````
node swap-sources.js
````

The script requires to `ANDROID_HOME` environment variable to be set and point towards the android-sdk directory.

## Usage
*Always make sure to restore the default naming with `-r` flag before executing any renaming action!*
Running the script without any parameters gives an "interactive" mode, asking which version your application compiles against (the _compileSdkVersion_) and which version the device you want to debug is running. Afterwards the folders will get renamed.

`-i` flag: Calling androud-source-swap -i will print a list of available Android SDK Version sources and the current folder naming.

`-r` flag: Use this flag to repair and restore any previously done renaming. It will name to folders like Android Studio expect them.

`-c [version int]` flag: Check whether a given Android SDK Version is installed. If it is installed the full SDK path will be returned.

Flags are not combinable. The first one will be consumed, all subsequent will get ignored.

`[project SDK version] [device SDK version]` quick mode: immediately provide the two Android SDK Versions that would be entered to the questions of the "interactive" guide. The script will rename the folders accordingly.