# blukii-sdk

blukii-sdk is the library for discovery and connection based configuration of blukii modules.


## Documentation and support

To learn about the usage of the library classes please find the [library's javadoc documentation](https://schneiderma.github.io/blukii_developer/android/blukii-sdk/javadoc/).

We recommend you to start with the following documentation pages where you can find some sample code fragments:
- package **info**: class [info/BlukiiClient](https://schneiderma.github.io/blukii_developer/android/blukii-sdk/javadoc/com/blukii/sdk/info/BlukiiClient.html), for discovery of Bluetooth LE modules (especially for blukiis) and detection of their emitting data like blukii configuration values, beacon sensor data and data of the standard protocols Eddystone and iBeacon. Furthermore this library lets you retrieve location based information that is assigned to any blukii on the [blukii Info Manager](https://manager.blukiiinfo.com).
- package **config**: class [config/Blukii](https://schneiderma.github.io/blukii_developer/android/blukii-sdk/javadoc/com/blukii/sdk/config/Blukii.html), for connection based configuring of core blukii and type-based settings for SmartBeacon, SmartKey and SmartSensor modules. 

For further question please contact the blukii developer support at [support@blukii.com](mailto:support@blukii.com).

## History

If you are already using our blukii-info-sdk, please note that it has been moved into blukii-sdk package **info**, containing the compatible object model.

Follow the steps to switch from blukii-info-sdk to blukii-sdk:
1. Replace the dependency from  'com.blukii:blukii-info-sdk:1.0.x' to 'com.blukii:blukii-sdk:1.0.1'
2. Find and Replace the package name all dependent import statements from 'com.blukii.infosdk' to 'com.blukii.sdk.info'.

## Changelog
### Version 1.0.1
First version

### Version 1.0.2
- package info: compatibility for new Info Manager Update of Aug 2017
- Bug fixes

## Getting started

Please follow the instructions for using the blukii-sdk in your Android Studio project.

### Android version

The minimum Android version is 4.4 Kitkat (API level 19) and the device has to support Bluetooth LE 4.0.

### Dependencies

The blukii-sdk can be easily integrated by adding the following dependency to your module's build.gradle:
```
 dependencies {
    ...
    compile 'com.blukii:blukii-sdk:1.0.1'
    ...
 }
```


### Permissions

For Bluetooth LE you need to insert the following permissions to your AndroidManifest.xml:
```
    <uses-permission android:name="android.permission.BLUETOOTH" />
    <uses-permission android:name="android.permission.BLUETOOTH_ADMIN" />
```

For Apps with **targetSdkVersion 23** (Android 6) and later you need to add a third permission:
```
    <uses-permission android:name="android.permission.ACCESS_COARSE_LOCATION" />
```
Please be aware that you have to handle "Runtime Permissions" in your App since Android 6. This [blog](https://inthecheesefactory.com/blog/things-you-need-to-know-about-android-m-permission-developer-edition/en) gives you a good instruction.


If you want to resolve data from the [blukii Info Manager](https://manager.blukiiinfo.com) (package **info**) you need to add the following:
```
    <uses-permission android:name="android.permission.INTERNET" />
```

### Ready!

Now you are ready to start developing your blukii App!

The [library's javadoc documentation](https://schneiderma.github.io/blukii_developer/android/blukii-sdk/javadoc/) should help you to understand developing based on blukii technology.
