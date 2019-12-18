
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

### AndroidX repositories

```	
repositories {

    maven { url 'https://gyant.mycloudrepo.io/public/repositories/mobile_sdk' }
    maven { url 'http://download.flutter.io' }
}
```	

GyantChatSDK does not support the simulator archs in release mode. To allow the integration of the SDK and further tests in the simulator we have created separated debug and release versions of the SDK. 

```
    def gyantSDKVersion="1.1.0"
    debugImplementation "com.gyant.gyant_chat_sdk:gyant_chat_sdk_debug:$gyantSDKVersion"
    releaseImplementation "com.gyant.gyant_chat_sdk:gyant_chat_sdk_release:$gyantSDKVersion"
    implementation "com.google.android.gms:play-services-location:17.0.0"
```

### Support repositories

```	
repositories {

    maven { url 'https://gyant.mycloudrepo.io/public/repositories/mobile_sdk_support' }
    maven { url 'http://download.flutter.io' }
}
```	

GyantChatSDK does not support the simulator archs in release mode. To allow the integration of the SDK and further tests in the simulator we have created separated debug and release versions of the SDK. 

```
    def gyantSDKVersion="1.1.0"
    debugImplementation "com.gyant.gyant_chat_sdk:gyant_chat_sdk_debug:$gyantSDKVersion"
    releaseImplementation "com.gyant.gyant_chat_sdk:gyant_chat_sdk_release:$gyantSDKVersion"
    implementation "com.google.android.gms:play-services-location:16.0.0"
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
    GyantChat gyantChat = GyantChat.getInstance()
                .clientId("client_id")
                .isDev(true)
                .start();
    
}
```

### Customize Appearance

```
@Override
protected void onCreate(Bundle savedInstanceState) {
    super.onCreate(savedInstanceState);

    // ...
    Map botPalette = new HashMap<String, String>();
    botPalette.put("primaryColor1","ff0000");

    Map providerPalette = new HashMap<String, String>();
    botPalette.put("primaryColor1","00ff00");


    Map themeMap = new HashMap<String, Map<String, String>>();
    themeMap.put("bot", botPalette);
    themeMap.put("provider", providerPalette);

    GyantChat gyantChat = GyantChat.getInstance()
                .clientId("client_id")
                .withTheme(themeMap)
                .isDev(true)
                .start();
```

 For more details about theme configuration read [here](#theme-configuration).

**Note**: The isDev parameter must be set to false before submitting the app to production.

### Listen to SDK data

```
public class YourActivity extends AppCompatActivity 
	implements GyantChatListener {

	@Override
	protected void onCreate(Bundle savedInstanceState) {
	    super.onCreate(savedInstanceState);

	    // ...

	    GyantChat gyantChat = GyantChat.getInstance()
			.clientId("client_id")
			.listener(this)
			.isDev(true)
			.start();
	    // ...
	}

	@Override
	public void getToken(CompletionHandler callback){
		callback.onComplete("token123");
	}

	@Override
	public void onMessage(String message) {
		// place your code here
	}

	@Override
	public void onDiagnosis(Map diagnosis)
		// place your code here
	}
}
```

### Changing patient data

All the fields available in GyantChatPatientData are optional. 

```
GyantChat.getInstance().changePatientData(<NEW-PATIENT-DATA>)	
```

<table>
<tr>
	<th>Field</th>
	<th>Description</th>
</tr>
<tr>
    <td>patientId</td>
    <td>Patient ID on the client’s side and can be any string/format. Max. lenght is 4096</td>
</tr>
<tr>
	<td>name</td>
    <td>Patient full name</td>
</tr>
<tr>
	<td>firstName</td>
    <td>Patient first name</td>
</tr>
<tr>
	<td>lastName</td>
    <td>Patient last name</td>
</tr>
<tr>
	<td>gender</td>
    <td>Patient gender, e.g: male or female.</td>
</tr>
<tr>
	<td>phone</td>
    <td>Patient phone number</td>
</tr>
<tr>
	<td>dateOfBirth</td>
    <td>Patient date of birth. Can use UTC, e.g. 2019-03-26T20:28:32.383+0000</td>
</tr>
<tr>
	<td>visitReason</td>
    <td>Patient visit reason if known</td>
</tr>
</table>

**Note**: When the patient data is changed the sdk will start a new conversation and lose the last conversation's history.


## Present Chat Interface

For presenting the chat interface GyantChatSDK provides three different methods.

### Gyant View

```
private GyantView gyantView;

...

gyantView = GyantChat.createView(this, getLifecycle());
FrameLayout frameLayout = (FrameLayout) findViewById(R.id.someContainer);
frameLayout.addView(gyantView);

...

@Override
public void onRequestPermissionsResult(int requestCode, @NonNull String[] permissions, @NonNull int[] grantResults) {
    gyantView.onRequestPermissionsResult(requestCode, permissions, grantResults);
}

```

### Gyant Fragment

```
private GyantFragment frag;

...

frag = GyantChat.createFragment();  

getSupportFragmentManager()  
    .beginTransaction()  
    .add(R.id.someContainer, frag,  BuildConfig.APPLICATION_ID + ".GyantFragment")  
    .commit();
    
...

@Override
public void onRequestPermissionsResult(int requestCode, @NonNull String[] permissions, @NonNull int[] grantResults) {
    frag.onRequestPermissionsResult(requestCode, permissions, grantResults);
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

## Theme Configuration

To allow a more seamless integration into existing apps, the SDK supports color customization. Currently, two different palletes are available: bot and provider. The bot palette is used during chat bot conversations while the provider will be loaded when the user is talking to a human (doctor, nurse, etc).

For each palette the following RGB colors could be customized:

<table>
  <tr>
    <th>Name</th>
    <th>Description</th>
    <th>bot</th>
    <th>provider</th>
  </tr>
  <tr>
    <td>primaryColor1</td>
    <td><ul><li>Background color</li><li>Auto-complete matches highlight text color</li><li>Hyperlink text color</li></ul></td>
    <td>ff4cb9f7</td>
    <td>ff1f5075</td>
  </tr>
  <tr>
    <td>primaryColor2</td>
    <td>Clinic and Provider cards text color</td>
    <td>ff3ea9f5</td>
    <td>ff3ea9f5</td>
  </tr>
  <tr>
    <td>primaryColor3</td>
    <td>n/a</td>
    <td></td>
    <td></td>
  </tr>
  <tr>
    <td>primaryColor4</td>
   <td><ul><li>QuickResponses bubble background color</li><li>Input box background color</li><li>User bubble background color</li></td>
    <td>ff79c7ff</td>
    <td>ff296a9c</td>
  </tr>
  <tr>
    <td>secondaryColor1</td>
    <td><ul><li>Auto-complete list background color</li><li>Connecting indicator background color</li><li>Scroll to bottom button icon color</li><li>Send button enabled icon color</li><li>Input box cursor color</li><li>Undo button icon color</li></ul></td>
    <td>ffffffff</td>
    <td>ffffffff</td>
  </tr>
  <tr>
    <td>secondaryColor2</td>
    <td>Success notification background color</td>
    <td>ff4cd964</td>
    <td>ff4cd964</td>
  </tr>
  <tr>
    <td>secondaryColor3</td>
    <td>Error notification background color</td>
    <td>fff55040</td>
    <td>fff55040</td>
  </tr>
  <tr>
    <td>secondaryColor4</td>
    <td>Provider bubble background color</td>
    <td>ff62849e</td>
    <td>ff62849e</td>
  </tr>
  <tr>
    <td>extraColor1</td>
    <td><ul><li>Card title text color</li><li>Connecting indicator text color</li><li>Auto-complete non-matches text color</li><li>Provider avatar placeholder initials text color</li></ul></td>
    <td>ff13324a</td>
    <td>ff0f77c6</td>
  </tr>
  <tr>
    <td>extraColor2</td>
    <td>Card subtitle text color</td>
    <td>ff767676</td>
    <td>ff767676</td>
  </tr>
  <tr>
    <td>extraColor3</td>
    <td>Send button disabled icon color</td>
    <td>ffaaaaaa</td>
    <td>ffaaaaaa</td>
  </tr>
  <tr>
    <td>extraColor4</td>
    <td>Provider avatar placeholder background color.</td>
    <td></td>
    <td></td>
  </tr>
  <tr>
    <td>extraColor5</td>
   <td><ul><li>Scroll to bottom button background color</li><li>Send button background color</li></td>
    <td>ff13324a</td>
    <td>ff13324a</td>
  </tr>
</table>



**Copyright © 2019 GYANT.com, Inc. All rights reserved.**
