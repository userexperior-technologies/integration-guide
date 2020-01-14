# Native iOS

## Integration
	
You can install the UserExperior iOS SDK through [cocoapods](https://cocoapods.org/) or manually.

**Via Cocoapods**

1. Install [cocoapods](https://cocoapods.org/) if you don't already have it.
2. Add to the pod file

<!-- - For swift 4.2 (Without IFA)
    ```
    pod 'UserExperior', '4.1.39' 
    ```
-->
 - For swift 5.0
 - 
    ```
    pod 'UserExperior', '4.1.61' 
    ```
    
 - For swift 5.1
 - 
    ```
    pod 'UserExperior', '4.1.62' 
    ```
    
 - For swift 5.1.2
 - 
    ```
    pod 'UserExperior', '4.1.59' 
    ```

    - For swift 5.1.3
    - 
       ```
       pod 'UserExperior', '4.1.64' 
       ```
3. From your terminal, type 

	- `pod repo update` (Optional - mostly if you are facing [Unable to find a specification in CocoaPods](https://stackoverflow.com/questions/25913733/unable-to-find-a-specification-in-cocoapods) issue)

		After repo update perform below command to install pod

	- `pod install`
4. Set `Always Embed Swift Standard Libraries` to `Yes` in Build Setting panel of project as well as app target. (Specially if your project based on old objective c project)

**Via Manual**

`Note: Framework support device architecture only means it will run only on device.`

1. Follow below link to download
	- [Download](https://userexperior-35559.firebaseapp.com/download/ios_sdk/4.1.29/UserExperior.zip)

2. Unzip the file and drag the UserExperior.framework directory to the “Frameworks” in your XCode project tree.
3. In your xcode project, select your application project in the Project Navigator (blue project icon) to navigate to the target configuration window and select the application target under the `Targets` heading in the sidebar.
4. In the tab bar at the top of that window, open the `General` panel.
5. Click on the + button under the `Embedded Binaries` section.
6. You will see UserExperior.framework nested inside a `Frameworks`.
7. Select the UserExperior.framework and click `Add`.
8. Set `Always Embed Swift Standard Libraries` to `Yes` in Build Setting panel of project as well as app target. (Specially if your project based on old objective c project)

And that's it!

The UserExperior.framework is automagically added as a target dependency, linked framework and embedded framework in a copy files build phase which is all you need to build on the simulator and a device.


**After SDK Integration (Via cocoapods)**

1. In your app delegate, include:

	- For Objective-C
	    
	    `#import <UserExperior/UserExperior-Swift.h>`

	- For Swift

	    `import UserExperior`

2. Add this call as the first line of your `application:didFinishLaunchingWithOptions:` method. 

	- For Objective-C

	    `[UserExperior initialize:@"USER_KEY"];`

	- For Swift

	    `UserExperior.initialize("USER_KEY")`


# Customizing UserExperior with Key APIs

## 1. Add User Identifier

UserExperior SDK by default takes device id as user identifier. However, you can specify any unique user identifier of your choice (eg. Email Id, Phone Number, etc.) as custom user identifier. This identifier will show up in UserExperior portal.

- For Objective-C
```
    [UserExperior setUserIdentifier:@"pass-your-user-id-here"];
```

- For Swift

```swift
    UserExperior.setUserIdentifier("pass-your-user-id-here")
```

## 2. Mask Sensitive Views

UserExperior SDK by default masks all the UITextField and UITextView. If you wish to mask any other UI element in your app, you can mask it by:

```swift
    let label = UILabel() 
    label.isSecureView = true
```

NOTE : Call `isSecureView` on any UI control object which is inherited from UIView

## 3. Control Recording

UserExperior SDK has following APIs which can be used to control the recording. The APIs stopRecording, pauseRecording, resumeRecording are optional and they should be only called when you explicitly want to override the default behavior. Basically, you can use pauseRecording and resumeRecording to bypass any user flow which you don't want UserExperior to capture


### Stop Recording
By default, recording stops automatically once the app goes to background. However, you can stop at desired point by calling this API.

- For Objective-C
```
    [UserExperior stopRecording];
```

- For Swift
```swift
    UserExperior.stopRecording()
```

### Pause Recording
This API pauses the recording, you can use resumeRecording API to resume.

- For Objective-C
```
    [UserExperior pauseRecording];
```

- For Swift
```swift
    UserExperior.pauseRecording()
```

### Resume Recording
This API resumes the recording if it is paused.

- For Objective-C
```
    [UserExperior resumeRecording];
```

- For Swift
```swift
    UserExperior.resumeRecording()
```

### Opt-In/Opt-Out

SDK by default opts-in users for session recording on app installs. If the user was disabled for session recording by using the optOut() method, you can use this method to enable recording at runtime.

- For Objective-C
```
    [UserExperior optIn];
```

- For Swift
```swift
    UserExperior.optIn()
```


This method returns the status of the user whether user is currently opted-in or opted-out. Boolean value true indicates that user is opted-out and false indicates that user is opted-in. 

- For Objective-C
```
    [UserExperior getOptOutStatus];
```

- For Swift
```swift
    UserExperior.getOptOutStatus()
```

## User Consent before recording 

As per GDPR guidelines, we have implemented a new feature called User Consent. This feature enables you to take consent from user before starting the session recording of that user. This will show a popup to the user on app launch, asking permission to track users app screen, gestures, in-app activities. If the user does not provide a consent then that users session and users details will not be recorded in the future. We recommend user consent to be taken on app launch, after starting UserExperior SDK you can make call to consent API: 

- For Objective-C
```
    [UserExperior consent];
```

- For Swift
```swift
    UserExperior.consent()
```


---

## `Important` - App transport security setting

If you are using Xcode 8.0 and Swift 3.0 or Swift 2.2 or even Objective C then add this in the plist:

```
<key>App Transport Security Settings</key>
<dict>
     <key>Allow Arbitrary Loads</key><true/>
</dict>
```

### What is NSAllowsArbitraryLoads? 
A Boolean value used to disable App Transport Security for any domains not listed in the NSExceptionDomains dictionary. Listed domains use the settings specified for that domain. The default value of NO requires the default App Transport Security behaviour for all connections.

More reference:

- [Stackoverflow](https://stackoverflow.com/questions/31254725/transport-security-has-blocked-a-cleartext-http)

