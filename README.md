Gyant Android SDK
==================

![Logo](https://gyant.com/wp-content/uploads/2018/10/Gyant.Logotype.HorizontalLeft@2x-1.png)

# About

GYANT combines messaging, AI, and medical experts to radically improve the diagnosis and treatment of non-urgent conditions. GYANT makes treatment faster, more effective & more delightful. Our purpose is to transform healthcare from the outside in — to create a new care standard for everyone.

# Requirements
 - Android 5.0
 - minSdkVersion 21
 - Android Studio 3.4.+

# Get aar
On https://github.com/GYANTINC/gyant-android-sdk download the release and debug gyant's sdks aar.

# Config project
Add both files to libs folder, then go to project structure and add an new jar dependency:
- add libs/gy_module-debug.aar and on step 2 set debugImplementation
- add libs/gy_module-release.aar and on step 2 set releaseImplementation

# Extra
- Disable IOT on android studio

In case the host app doesn't have the following api the developer should add them
- api 'com.google.android.gms:play-services-location:16.+'
- api "androidx.biometric:biometric:1.0.0-alpha04"

- add build.gradle
	compileOptions {
        sourceCompatibility 1.8
        targetCompatibility 1.8
    }

- add to manifest
    <uses-permission android:name="android.permission.INTERNET" />
    <uses-permission android:name="android.permission.ACCESS_NETWORK_STATE" />
    <uses-permission android:name="android.permission.ACCESS_FINE_LOCATION" />
