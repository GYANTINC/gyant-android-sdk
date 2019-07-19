
Gyant Android SDK
==================

![Logo](https://gyant.com/wp-content/uploads/2018/10/Gyant.Logotype.HorizontalLeft@2x-1.png)

  

# About

GYANT combines messaging, AI, and medical experts to radically improve the diagnosis and treatment of non-urgent conditions. GYANT makes treatment faster, more effective & more delightful. Our purpose is to transform healthcare from the outside in — to create a new care standard for everyone.

  

# Requirements

- Android 5.0

- minSdkVersion 21

- Android Studio 3.4.+

  
Gyant SDK is compatible with Android 5.0 (API Level 21) and higher.

# Getting Started

## Download binaries

On https://github.com/GYANTINC/gyant-android-sdk download the release and debug aar versions.

## Copy binaries

Add both files to libs folder in your project directory.

## Edit your app's build.gradle
	
Using Gyant might require you to enable Java 8 support through desugaring in your project.
You might need to add the following in your build.gradle:

```	
android {
	compileOptions {
		sourceCompatibility 1.8
		targetCompatibility 1.8
	}
```

GyantChatSDK does not support the simulator archs in release mode. To allow the integration of the SDK and further tests in the simulator we have created separated debug and release versions of the SDK. 

```
dependencies {
    debugImplementation files('libs/gyantchatsdk-debug.aar')
    releaseImplementation files('libs/gyantchatsdk-release.aar')
```

In order to work correctly, GyantChat requires firebase-core and firebase-messaging 11.0.0 or higher. We highly recommend to use the latest version when possible. Add the following to your build.gradle, if not already present:

```
dependencies {
...		
	 api 'com.google.android.gms:play-services-location:16.+'
	 api 'androidx.biometric:biometric:1.0.0-alpha04'
```


## Edit manifest permissions

Add the following permissions to your manifest file.

```	
<uses-permission  android:name="android.permission.INTERNET"/>
<uses-permission  android:name="android.permission.ACCESS_NETWORK_STATE"/>
<uses-permission  android:name="android.permission.ACCESS_FINE_LOCATION"/>
<uses-permission android:name="android.permission.VIBRATE"/>
```

# Getting Started

### Create a view

```
@Override  
protected void onCreate(Bundle savedInstanceState) {  
	super.onCreate(savedInstanceState);  
	setContentView(R.layout.activity_display_gyant_view);
	
	GyantChat gyantChat = new GyantChat();
	gyantChat.gyantChatInit("<YOUR-CLIENT-ID>",  "<YOUR-PATIENT-ID>", true);
}
```

**Note**: The isDev parameter must be set to false before submitting the app to production.

### Create a Fragment

```
@Override  
protected void onCreate(Bundle savedInstanceState) {  
    super.onCreate(savedInstanceState);  
    setContentView(R.layout.activity_display_fragment);  
  
    GyantChat gyantChat = new GyantChat();  
    gyantChat.gyantChatInit("<YOUR-CLIENT-ID>",  "<YOUR-PATIENT-ID>", true);  
  
    Fragment frag = gyantChat.gyantChatFragment();  
  
    getSupportFragmentManager()  
            .beginTransaction()  
            .add(R.id.frame_layout, frag,  BuildConfig.APPLICATION_ID + ".GyantFragment")  
            .commit();  
}
```
**Note**: The isDev parameter must be set to false before submitting the app to production.

### Create an Activity

```
public class DisplayGyantChatActivity extends GyantChatActivity {  
  
    @Override  
    protected void onCreate(Bundle savedInstanceState) {  
		//gyantChatInit should be called before onCreate
		new GyantChat().gyantChatInit("<YOUR-CLIENT-ID>",  "<YOUR-PATIENT-ID>", isDev);  
		super.onCreate(savedInstanceState);  
    }  
}
```
**Note**: The isDev parameter must be set to false before submitting the app to production and gyantChatInit should be called before onCreate.


## Include the SDK for Android in an Existing Application

The  [samples](https://github.com/GYANTINC/gyant-android-sdk-samples)  included with the SDK for Android are standalone projects that are already set up for you. You can also integrate the SDK for Android with your own existing project.


**Copyright © 2019 GYANT.com, Inc. All rights reserved.**
