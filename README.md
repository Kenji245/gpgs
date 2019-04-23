# ![logo](./logo.png) godot-GamePlayGoogleServices

[![Platform](https://img.shields.io/badge/Platform-Android-green.svg?longCache=true&style=flat-square)](https://github.com/xsellier/godotandroid)
[![Godot Engine](https://img.shields.io/badge/GodotEngine-2.1-orange.svg?longCache=true&style=flat-square)](https://github.com/godotengine/godot)
[![Godot Engine](https://img.shields.io/badge/GodotEngine-3.x-orange.svg?longCache=true&style=flat-square)](https://github.com/godotengine/godot)
[![LICENCE](https://img.shields.io/badge/License-MIT-green.svg?longCache=true&style=flat-square)](https://github.com/xsellier/godotandroid/blob/master/LICENSE)

# Forked by

Kopfenheim GitHub: `git clone https://github.com/Kopfenheim/godot-gpgs` at 4 May 2019

See in [English](https://github.com/ClaudioEden/godot-GamePlayGoogleServices#google-play-game-services-android-for-godot-game-engine) :us:   /   Leia em [Português](https://github.com/ClaudioEden/godot-GamePlayGoogleServices#modulo-google-play-game-services-para-engine-godot-android) <span>&#x1f1e7;&#x1f1f7;</span>


# Google Play Game Services (Android) for Godot Game Engine

This is a Google Play Game Services module for the Godot Game Engine. This module is meant to be used for games deployed to an Android device. This module allows you to use nearly all the features provided by the Google Play Games Service API for Android including:
- Log-in with Google
- Information about the signed in player (including their profile pictures)
- Achievements
- Leaderboards
- Saved Games (Snapshots)
- Real Time Multiplayer
- Device network status

This module uses Google Play Services' powerful Tasks API to execute various operations asynchronously. To handle the results from these asynchronous operations, a lot of relevant callback functions are also provided and can be used in GDScript.

**NOTE:** This module is compatible with Godot 3.1 but has not been tested with the Mono version. So, using this module for developing Godot games using C# could lead to unforeseen errors.

**NOTE"** This is compatible with Admob from https://github.com/kloder-games/godot-admob and does work for both.

## Setup
1. Make sure that you have the Android SDK and NDK setup and are familiar with compiling Godot for Android (See Godot's documentation for more information about this)
2. Create a "Game Services" game in the Google Play Console and take a note of the App ID
3. Clone or download the repository onto your computer
4. Copy the "gpgs" folder into the "modules" directory of Godot's source code
5. Inside "../android/AndroidManifestChunk.xml", replace the `{Your APP_ID here}`, dont remove `\u003` so that it looks more like this (note: the APP_ID shown here is just a dummy value) (note2: the last tag fixes a crash with Android 9)

	```xml
	<meta-data android:name="com.google.android.gms.games.APP_ID" android:value="\u0031234567890123" />
	<meta-data android:name="com.google.android.gms.version" android:value="@integer/google_play_services_version"/>
	<uses-library android:name="org.apache.http.legacy" android:required="false"/>
	```

6. If any of your other modules also use the second line of the AndroidManifestChunk.xml shown above, then delete one of them because it could cause errors down the line.
7. If you are trying to use the same admob modules that I mentoined you need to remove this line from `/platform/android/java/build.gradle`
	```
	dependencies {
		// implementation "com.android.support:support-core-utils:28.0.0"
		compile ('com.google.android.gms:play-services-ads:16.0.0') { exclude group: 'com.android.support' }
		compile 'com.google.android.gms:play-services-auth:16.0.0'
		compile 'com.google.android.gms:play-services-games:16.0.0'
	}
	```
8. Recompile the Godot source for android
9. Compile the resultant Android project using `gradlew build`.
10. Open the godot engine and link the created .apk files as Custom Packages in the Export menu
11. Enable the following permissions in the Export menu
	- Access Network State
	- Internet

## Using the module in your game
1. Add the following code in your project's engine.cfg file (for Godot versions lower than 3.0) or in the project.godot file (for Godot 3.0 and above)

	```
	[android]

	modules="org/godotengine/godot/GodotPlayGameServices"
	```
	**NOTE** if you are using admob it would look like this ;
	```
	[android]

	modules="org/godotengine/godot/GodotPlayGameServices,org/godotengine/godot/GodotAdMob"
	```
2. If you already have such an entry then add a `,` after the existing module path, followed `org/godotengine/godot/GodotPlayGameServices` in the string. It would look something like this:

	```
	[android]

	modules="{existing_module},org/godotengine/godot/GodotPlayGameServices"
	```
3. To use the module in GDScript:
	- Godot 3.0 or above (3.1 is compatible)
		```python
		if OS.get_name() == "Android":
			if Engine.has_singleton("GodotPlayGameServices"):
				gpgs = Engine.get_singleton("GodotPlayGameServices")
				gpgs.init(get_instance_id(), true)
		```
	- Godot versions lower than 3.0
		```python
		if(Globals.has_singleton("GodotPlayGameServices")):
			gpgs = Globals.get_singleton("GodotPlayGameServices")
			gpgs.init(get_instance_ID(), true)
		```
4. Now, you should be able to call the functions in the `gpgs` object (singleton) in order to use the Google Play Game Services.

## Functions and Callbacks
See the [Wiki](https://github.com/Kopfenheim/godot-gpgs/wiki) for a description of the various functions that you can call on the `gpgs` object and the various callbacks that you can listen for in your GDScript file


# Modulo Google Play Game Services para Engine Godot (Android)
