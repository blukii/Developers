# blukii-info-sdk BETA

blukii-info-sdk is the library for discovering Bluetooth LE modules (especially for blukiis) and reading their emitting data like blukii configuration values, beacon sensor data and data of the standard protocols Eddystone and iBeacon.

Furthermore this library lets you retrieve location based information that is assigned to any blukii on the [blukii Info Manager](https://manager.blukiiinfo.com).

## Documentation and support

BETA API Documentation: [blukiiInfoSDK Framework Reference](https://schneiderma.github.io/blukii_developer/iOS/blukii-Info-SDK/docs/)
                                                            
We recommend you to start with the documentation page of class [BKClient](https://schneiderma.github.io/blukii_developer/iOS/blukii-Info-SDK/docs/Classes/BKClient.html)

For further question please contact the blukii developer support at [support@blukii.com](mailto:support@blukii.com)

## Getting started 

Please follow the instructions for using the blukii-info-sdk in your xCode-Project.

### iOS Version

The minimum iOS Version is iOS 8.0

### Installion with CocoaPods
CocoaPods is a dependency manager for Swift and Objective-C Cocoa projects like the blukiiSK.  [Here](https://cocoapods.org) you will find more information about CocoaPod. 

Install cocoapods:
```
sudo gem install cocoapods
```


Generate a podfile for your xcode Project:
```
pod init
```

Insert the new depency to your Podfile:

```
target 'YourApp' do
pod 'blukiiInfoSDK', '~> 0.1.0-Beta2'
end
```

Then run the following command: 

```
pod install
```

If you have and Objective-C Project, you have to insert a Swift file with the automatic generated Objective-C-Bridging-Header.h or you set the setting "Always Embed Swift Standard Libraries" to "YES"

### Ready!

Now you are ready to start developing your blukii App!

The [blukiiInfoSDK Framework Reference](https://schneiderma.github.io/blukii_developer/iOS/blukii-Info-SDK/docs/) should help you to understand what are the right settings for your special use case.
