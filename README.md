
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

- add to app build.gradle file
	
	```	
	android {
		...
		compileOptions {
			sourceCompatibility 1.8
			targetCompatibility 1.8
		}
	```
	
	```
	dependencies {
	...		
		 api 'com.google.android.gms:play-services-location:16.+'
		 api "androidx.biometric:biometric:1.0.0-alpha04"
	 ```	


- add to manifest
	```	
	<uses-permission  android:name="android.permission.INTERNET"  />
	<uses-permission  android:name="android.permission.ACCESS_NETWORK_STATE"  />
	<uses-permission  android:name="android.permission.ACCESS_FINE_LOCATION"  />
	```	


# Getting Started

### Create a view

```
@Override  
protected void onCreate(Bundle savedInstanceState) {  
	super.onCreate(savedInstanceState);  
	setContentView(R.layout.activity_display_gyant_view);  
	  
	GyantChat gyantChat = new GyantChat();  
	gyantChat.gyantChatInit("client_id",  "pacient_id", isDev);  
	  
	View gyantView = gyantChat.gyantChatView(this, getLifecycle());  
	  
	FrameLayout frameLayout = (FrameLayout) findViewById(R.id.frame_layout);  
	frameLayout.addView(gyantView);  
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
    gyantChat.gyantChatInit("client_id",  "pacient_id", isDev);  
  
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
		new GyantChat().gyantChatInit("client_id",  "pacient_id", isDev);  
		super.onCreate(savedInstanceState);  
    }  
}
```
**Note**: The isDev parameter must be set to false before submitting the app to production and gyantChatInit should be called before onCreate.


## Include the SDK for Android in an Existing Application

The  [samples](https://github.com/GYANTINC/gyant-android-sdk-samples)  included with the SDK for Android are standalone projects that are already set up for you. You can also integrate the SDK for Android with your own existing project.


**Copyright © 2019 GYANT.com, Inc. All rights reserved.**
