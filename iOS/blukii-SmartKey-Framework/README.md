# blukii-SmartKey-Framework

blukii-SmartKey-Framwork is a framework for an easy use of our blukii SmartKey in your own app.  With the framework you can configure the blukii SmartKey and authenticate with the blukii SmartKey. 

## Documentation and support
To learn about the usage of the framework classees please find the [blukiiSK Framework Reference](https://schneiderma.github.io/blukii_developer/iOS/blukii-SmartKey-Framework/html/)

There you will also find sample code framgments and a demo project. 

## Getting started

Please follow the instructions for using the blukii-smartKey-framework in your xCode-Project. 

### iOS Version

The minimum iOS Version is iOS 8.4

### Installion with CocoaPods
CocoaPods is a dependency manager for Swift and Objective-C Cocoa projects like the blukiiSK.  [Here](https://cocoapods.org) you will find more information about CocoaPod. 

Generate a podfile for your xcode Project:
```
   pod init
```

Insert the new depency to your Podfile:

```
  pod 'blukiiSK'
```

Then run the following command: 

```
   pod install
```

For a Swift project you have to add an Bridiging-Header and import the blukiiSK:

```objective-c
#import <blukiiSK/blukiiSK.h>
```

### Ready!

Now you are ready to start developing your blukii App!

The [blukiiSK Framework Reference](https://schneiderma.github.io/blukii_developer/iOS/blukii-SmartKey-Framework/html/) should help you to understand what are the right settings for your special use case.  Here you will find a demo Project: [Demo Project](https://github.com/schneiderma/blukii_developer/raw/gh-pages/iOS/blukii-SmartKey-Framework/html/examples/blukiiSK_Demo.zip)