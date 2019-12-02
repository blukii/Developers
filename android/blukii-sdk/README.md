# blukii-sdk

blukii-sdk is the library for discovery and connection based configuration of blukii modules.


## Documentation and support

To learn about the usage of the library classes please find the [library's javadoc documentation](https://blukii.github.io/Developers/android/blukii-sdk/javadoc/).

We recommend you to start with the following documentation pages where you can find some sample code fragments:
- Package **discovery**: class [discovery/BlukiiClient](https://blukii.github.io/Developers/android/blukii-sdk/javadoc/com/blukii/sdk/discovery/BlukiiClient.html), for discovery of Bluetooth LE modules (especially for blukiis) and detection of their emitting data like blukii Beacon sensor data and data of the standard protocols Eddystone and iBeacon. Furthermore this package lets you decrypt encrypted blukii Secure Beacon advertising data by connecting to [blukii Manager](https://manager.blukii.com).
- Package **info**: class [info/BlukiiInfo](https://blukii.github.io/Developers/android/blukii-sdk/javadoc/com/blukii/sdk/info/BlukiiInfo.html), for retrieving and reporting location based information that is assigned to any blukii on the [blukii Manager Info CMS](https://manager.blukii.com).
- Package **config**: class [config/Blukii](https://blukii.github.io/Developers/android/blukii-sdk/javadoc/com/blukii/sdk/config/Blukii.html), for connection based configuring of core blukii and type-based settings for SmartBeacon, SmartKey and SmartSensor modules. Furthermore this package lets you synchronize configuration data with [blukii Manager](https://manager.blukii.com).

For further question please contact the blukii developer support at [support@blukii.com](mailto:support@blukii.com).

## Feature Licensing
You have to distinguish between basic and advanced features that are provided by blukii-sdk.

Basic features are free of charge: all offline features that have no need to communicate with [blukii Manager](https://manager.blukii.com):
- Discovery of blukii advertising Data (package **discovery**)
- Connection based configuration (package **config**)

For Advanced features a fee-based blukii API key is needed: all feature with connection to [blukii Manager](https://manager.blukii.com):
- Decryption of blukii Secure Beacons (package **discovery**)
- All features of package **info**
- Sync of connection based blukii configuration data with [blukii Manager](https://manager.blukii.com)

Please contact the blukii developer support at [support@blukii.com](mailto:support@blukii.com) for requesting an blukii API key.

## Changelog
### Version 2.0.2
- Hotfix: Exception when stopping discovery if BluetoothAdapter is disabled

### Version 2.0.1
- Hotfix: Exception when calling BlukiiClient.startDiscovery() and BlukiiClient.stopDiscovery() without running Bluetooth on device.

### Version 2.0.0
- Refactoring of package info: separation of **discovery** and **info** features in two functional separated packages. See javadoc of classes [discovery/BlukiiClient](https://blukii.github.io/Developers/android/blukii-sdk/javadoc/com/blukii/sdk/discovery/BlukiiClient.html) and [info/BlukiiInfo](https://blukii.github.io/Developers/android/blukii-sdk/javadoc/com/blukii/sdk/info/BlukiiInfo.html) for learning how to use it now.
- Support of Smart Beacon firmware 002.009, e.g.
  - blukii Secure Beacon
  - blukii Event Beacon
- Sync of connection based blukii configuration data with [blukii Manager](https://manager.blukii.com)
- Optimization of Bluetooth LE scan, especially of background scan
- Bug fixes

### Version 1.0.3
- Package info: termination of discovery (BlukiiClient) optimized
- Package config: compatibility to blukii beacon firmware version 00X.006
- Bug fixes

### Version 1.0.2
- Package info: compatibility for new Info Manager Update of Aug 2017
- Bug fixes

### Version 1.0.1
First version

## Getting started

Please follow the instructions for using the blukii-sdk in your Android Studio project.

### Android version

The minimum Android version is 4.4 Kitkat (API level 19) and the device has to support Bluetooth LE 4.0.

### Dependencies

The blukii-sdk can be easily integrated by adding the following dependency to your module's build.gradle:
```
 dependencies {
    ...
    compile 'com.blukii:blukii-sdk:2.0.2'
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


If you use advanced functions that communicate with [blukii Manager](https://manager.blukii.com) you need to add the following:
```
    <uses-permission android:name="android.permission.INTERNET" />
```

### Ready!

Now you are ready to start developing your blukii App!

The [library's javadoc documentation](https://blukii.github.io/Developers/android/blukii-sdk/javadoc/) should help you to understand developing based on blukii technology.
