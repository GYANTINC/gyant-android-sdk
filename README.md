
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
    sourceCompatibility JavaVersion.VERSION_1_8
    targetCompatibility JavaVersion.VERSION_1_8
  }
}
```

GyantChatSDK does not support the simulator archs in release mode. To allow the integration of the SDK and further tests in the simulator we have created separated debug and release versions of the SDK. 

```
dependencies {
    debugImplementation files('libs/gyantchatsdk-debug.aar')
    releaseImplementation files('libs/gyantchatsdk-release.aar')
```

GyantChat requires play-services-location.

```
dependencies {
    implementation 'com.google.android.gms:play-services-location:16.0.0'
}
```


## Edit manifest permissions

Add the following permissions to your manifest file.

```	
<uses-permission  android:name="android.permission.INTERNET"/>
<uses-permission  android:name="android.permission.ACCESS_NETWORK_STATE"/>
<uses-permission  android:name="android.permission.ACCESS_FINE_LOCATION"/>
<uses-permission  android:name="android.permission.VIBRATE"/>
```

# Getting Started

## Start the SDK

```
@Override  
protected void onCreate(Bundle savedInstanceState) {  
    super.onCreate(savedInstanceState);  
    
    // ...
    GyantChat.start("<YOUR-CLIENT-ID>",  "<YOUR-PATIENT-ID>", true);
    
}
```

**Note**: The isDev parameter must be set to false before submitting the app to production.

## Present Chat Interface

For presenting the chat interface GyantChatSDK provides three different methods.

### Gyant View

```
GyantView gyantView;

...

this.gyantView = GyantChat.createView(this, getLifecycle());
FrameLayout frameLayout = (FrameLayout) findViewById(R.id.someContainer);
frameLayout.addView(gyantView);

...

@Override
public void onRequestPermissionsResult(int requestCode, @NonNull String[] permissions, @NonNull int[] grantResults) {
    this.gyantView.onRequestPermissionsResult(requestCode, permissions, grantResults);
}

```

### Gyant Fragment

```
GyantFragment frag;

...

this.frag = GyantChat.createFragment();  

getSupportFragmentManager()  
    .beginTransaction()  
    .add(R.id.someContainer, frag,  BuildConfig.APPLICATION_ID + ".GyantFragment")  
    .commit();
    
...

@Override
public void onRequestPermissionsResult(int requestCode, @NonNull String[] permissions, @NonNull int[] grantResults) {
    this.frag.onRequestPermissionsResult(requestCode, permissions, grantResults);
}
```

### Gyant Activity

```
public class DisplayGyantChatActivity extends GyantChatActivity {  
  
    @Override  
    protected void onCreate(Bundle savedInstanceState) {  
    
    	// GyantChat.start must be called before onCreate
    	super.onCreate(savedInstanceState);  
    }
}
```


## Include the SDK for Android in an Existing Application

The  [samples](https://github.com/GYANTINC/gyant-android-sdk-samples)  included with the SDK for Android are standalone projects that are already set up for you. You can also integrate the SDK for Android with your own existing project.


**Copyright © 2019 GYANT.com, Inc. All rights reserved.**
