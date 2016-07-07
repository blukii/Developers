# blukii-info-sdk

blukii-info-sdk is the library for discovering Bluetooth LE modules (especially for blukiis) and reading their emitting data like blukii configuration values, beacon sensor data and data of the standard protocols Eddystone and iBeacon.

Furthermore this library lets you retrieve location based information that is assigned to any blukii on the [blukii Info Manager](https://manager.blukiiinfo.com).

## Documentation and support

To learn about the usage of the library classes please find the [library's javadoc documentation](https://schneiderma.github.io/blukii_developer/android/blukii-info-sdk/javadoc/).

We recommend you to start with the documentation page of class **BlukiiClient** where you can find some sample code fragments.

For further question please contact the blukii developer support at [support@blukii.com](mailto:support@blukii.com).

## Getting started

Please follow the instructions for using the blukii-info-sdk in your Android Studio project.

### Android version

The minimum Android version is 4.4 Kitkat (API level 19) and the device has to support Bluetooth LE 4.0.

### Dependencies

The blukii-info-sdk can be easily integrated by adding the following dependency to your module's build.gradle:
```
 dependencies {
    ...
    compile 'com.blukii:blukii-info-sdk:1.0.0'
    ...
 }
```


### Permissions

For the Bluetooth LE discovery you need to insert the following permissions to your AndroidManifest.xml:
```
    <uses-permission android:name="android.permission.BLUETOOTH" />
    <uses-permission android:name="android.permission.BLUETOOTH_ADMIN" />
```

If you want to resolve data from the [blukii Info Manager](https://manager.blukiiinfo.com) you need to add the following:
```
    <uses-permission android:name="android.permission.INTERNET" />
```

### Ready!

Now you are ready to start developing your blukii App!

The blukii-info-sdk gives you the possibility to vary several settings to fine tune the Bluetooth LE discovery and the data retrieving process. 

The [library's javadoc documentation](https://schneiderma.github.io/blukii_developer/android/blukii-info-sdk/javadoc/) should help you to understand what are the right settings for your special use case.
