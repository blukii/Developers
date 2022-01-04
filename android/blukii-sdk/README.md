# blukii-sdk

blukii-sdk is the library for discovery and connection based configuration of blukii modules.

## Documentation and support

To learn about the usage of the library classes please find the [library's javadoc documentation](https://blukii.github.io/Developers/android/blukii-sdk/javadoc/index.html).

We recommend you to start with the following documentation pages where you can find some sample code fragments:

- Package **discovery**: class [discovery/BlukiiClient](https://blukii.github.io/Developers/android/blukii-sdk/javadoc/com/blukii/sdk/discovery/BlukiiClient.html), for discovery of Bluetooth LE modules (especially for blukiis) and detection of their emitting data like blukii Beacon sensor data and data of the standard protocols Eddystone and iBeacon. Furthermore this package lets you decrypt encrypted blukii Secure Beacon advertising data by connecting to [blukii Manager](https://manager.blukii.com).
- Package **info**: class [info/BlukiiInfo](https://blukii.github.io/Developers/android/blukii-sdk/javadoc/com/blukii/sdk/info/BlukiiInfo.html), for retrieving and reporting location based information that is assigned to any blukii on the [blukii Manager Info CMS](https://manager.blukii.com).
- Package **config**: class [config/Blukii](https://blukii.github.io/Developers/android/blukii-sdk/javadoc/com/blukii/sdk/config/Blukii.html), for connection based configuring of core blukii and type-based settings for SmartBeacon, SmartKey and SmartSensor modules. Furthermore this package lets you synchronize configuration data with [blukii Manager](https://manager.blukii.com).

For further question please contact the blukii developer support at [support@blukii.com](mailto:support@blukii.com).

## Feature Licensing

Since version 4.0.0 a developer API key is mandatory for using blukii-sdk. You can create a free basic API key at [blukii Manager](https://manager.blukii.com) on your Account settings section API KEYS.

Basic API key allows to use the following blukii-sdk features:

- Discovery of blukii advertising Data (package **discovery**)
- Connection based configuration (package **config**) without data sync to [blukii Manager](https://manager.blukii.com).

For advanced features the API key has to assigned to additional fee-based permissions:

- All features of package **info**
- Connection based configuration (package **config**) with sync to [blukii Manager](https://manager.blukii.com).

Please contact the blukii developer support at [support@blukii.com](mailto:support@blukii.com) for requesting additional permissions.

## Getting started

Please follow the instructions for using the blukii-sdk in your Android Studio project.

### Android version

The minimum Android version is 4.4 Kitkat (API level 19) and the device has to support Bluetooth LE 4.0 or later.

### Gradle settings

The blukii-sdk can be easily integrated by adding the following parts to your module's build.gradle:

```text
android {
  ...
  compileOptions {
      sourceCompatibility JavaVersion.VERSION_1_8
      targetCompatibility JavaVersion.VERSION_1_8
  }
  ...
}
...
dependencies {
  ...
  implementation 'com.blukii:blukii-sdk:4.0.0'
  ...
}
```

### Permissions

You need to insert the following permissions to your AndroidManifest.xml:

```text
    <uses-permission android:name="android.permission.INTERNET" />
    <uses-permission android:name="android.permission.BLUETOOTH" />
    <uses-permission android:name="android.permission.BLUETOOTH_ADMIN" />
```

For Apps with **targetSdkVersion 23** (Android 6) and later you need to add the following permission:

```text
    <uses-permission android:name="android.permission.ACCESS_FINE_LOCATION" />
```

For Apps with targetSdkVersion 29 (Android 10) and later that should use discovery in background you additionally have to handle the following permission in combination with **ACCESS_FINE_LOCATION**.
Therefore please read Google's manual about [access to device location in the background](https://developer.android.com/about/versions/10/privacy/changes#app-access-device-location).

```text
    <uses-permission android:name="android.permission.ACCESS_BACKGROUND_LOCATION" />
```

Please be aware that you have to handle "Runtime Permissions" in your App since Android 6. This [blog](https://inthecheesefactory.com/blog/things-you-need-to-know-about-android-m-permission-developer-edition/en) gives you a good instruction.

### API key setting

You need to insert the following meta-data part to application settings of your AndroidManifest.xml:

```text
    <application
        android:name=".YourApp"
        ...
        >

        <meta-data android:name="com.blukii.sdk.API_KEY"
            android:value="<your API key>"/>

        ...
    </application>
```

### Ready

Now you are ready to start developing your blukii App!

The [library's javadoc documentation](https://blukii.github.io/Developers/android/blukii-sdk/javadoc/index.html) should help you to understand developing based on blukii technology.

## Changelog

### Version 4.0.0

- New [Feature Licensing](#Feature-Licensing) prodecure based on API key. For update to 4.0.0 please check [Getting Started](#Getting-Started).
- Support of blukii BLE 5.x firmware.
- Package config: Blukii.updateFirmware() for updating BLE 5.x firmware version via blukii Manager.
- Code refactorings and optimizations

### Version 3.1.2

- DiscoverySettings.setScanFilters added: optimize ScanFilters for BLE discovery

### Version 3.1.1

- Hotfix discovery: Scan is off on background or screen off if DiscoverySettings.setProfile(DiscoveryProfile.CONTINUOUS) is set

### Version 3.1.0

- Package config: Blukii.updateData() for synchronizing cloud data to blukii device
- Bug fixes: internal discovery and connection error handling

### Version 3.0.1

- Hotfix: ClassNotFoundException because of missing library dependency

### Version 3.0.0

- AndroidX: Version 3.0.0 requires the migration of your app to AndroidX. See [Migrating to AndroidX](https://developer.android.com/jetpack/androidx/migrate).
- BlukiiController: new main controller of blukii SDK: get instances of package controllers ([BlukiiCloud](https://blukii.github.io/Developers/android/blukii-sdk/javadoc/com/blukii/sdk/cloud/BlukiiCloud.html), [BlukiiClient](https://blukii.github.io/Developers/android/blukii-sdk/javadoc/com/blukii/sdk/discovery/BlukiiClient.html), [BlukiiInfo](https://blukii.github.io/Developers/android/blukii-sdk/javadoc/com/blukii/sdk/info/BlukiiInfo.html), [Blukii](https://blukii.github.io/Developers/android/blukii-sdk/javadoc/com/blukii/sdk/config/Blukii.html)) via BlukiiController only.
- Package discovery:
  - optimized background discovery for new Android versions
  - DiscoverySettings: new [DiscoveryProfile](https://blukii.github.io/Developers/android/blukii-sdk/javadoc/com/blukii/sdk/discovery/BlukiiClient.html) replaces separate setting of scan types for foreground, background and screen off
  - BlukiiClient: simplified initialization and start/stop of discovery
  - permission ACCESS_FINE_LOCATION required
  - permission ACCESS_BACKGROUND_LOCATION for Android 10 and later
- Package Info:
  - resolve InfoBundles from [blukii Manager](https://manager.blukii.com): see [BlukiiInfo](https://blukii.github.io/Developers/android/blukii-sdk/javadoc/com/blukii/sdk/info/BlukiiInfo.html) documentation

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
