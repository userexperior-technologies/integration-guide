# Native - iOS

### Integration
    
You can install the UserExperior iOS SDK through [cocoapods](https://cocoapods.org/) or manually.

####  Via Cocoapods

> Note: Install [cocoapods](https://cocoapods.org/) if you don't already have it.

1. Add to the pod file

     **For swift 5.2+**
 
         pod 'UserExperior', '4.4.18' 

     **For swift 5.1.2 & 5.1.3**
    
        pod 'UserExperior', '4.4.17' 

     **For swift 5.1 & below**
    
        pod 'UserExperior', '4.4.16' 



2. From your terminal, type 

        pod install
           

3. In your app delegate, include:

- 3. a. For Objective-C
    
            #import <UserExperior/UserExperior-Swift.h>

-  3. b. For Swift

            import UserExperior

4. Add this call as the first line of your `application:didFinishLaunchingWithOptions:` method. 

- 4. a. For Objective-C

            [UserExperior initialize:@"USER_KEY"];
    `Note: After integration perform the test ONLY on REAL iOS DEVICES since framework support device architecture. After performing activities minimize the app. UserExperior will upload the data, which could be seen within 2-3 minutes on the UserExperior portal.`

- 4. b. For Swift

            UserExperior.initialize("USER_KEY")
    `Note: After integration perform the test ONLY on REAL iOS DEVICES since framework support device architecture. After performing activities minimize the app. UserExperior will upload the data, which could be seen within 2-3 minutes on the UserExperior portal.`


#### Via Manual
1. Follow below link to download
- [Download (For Swift 5.2.+)](https://userexperior-e174e.firebaseapp.com/download/ios_sdk/4.4.18/UserExperior.zip)
- [Download (For Swift 5.1.2 & 5.1.3)](https://userexperior-e174e.firebaseapp.com/download/ios_sdk/4.4.17/UserExperior.zip)
- [Download (For Swift 5.1 & Below)](https://userexperior-e174e.firebaseapp.com/download/ios_sdk/4.4.16/UserExperior.zip)

2. Unzip the file and drag the UserExperior.framework directory to the “Frameworks” in your XCode project tree.
3. In your xcode project, select your application project in the Project Navigator (blue project icon) to navigate to the target configuration window and select the application target under the `Targets` heading in the sidebar.
4. In the tab bar at the top of that window, open the `General` panel.
5. Click on the + button under the `Embedded Binaries` section.
6. You will see UserExperior.framework nested inside a `Frameworks`.
7. Select the UserExperior.framework and click `Add`.
8. In your app delegate, include:

- 8. a. For Objective-C
    
            #import <UserExperior/UserExperior-Swift.h>

-  8. b. For Swift

            import UserExperior

9. Add this call as the first line of your `application:didFinishLaunchingWithOptions:` method. 

- 9. a. For Objective-C

            [UserExperior initialize:@"USER_KEY"];
    `Note: After integration perform the test ONLY on REAL iOS DEVICES since framework support device architecture. After performing activities minimize the app. UserExperior will upload the data, which could be seen within 2-3 minutes on the UserExperior portal.`

- 9. b. For Swift

            UserExperior.initialize("USER_KEY")
    `Note: After integration perform the test ONLY on REAL iOS DEVICES since framework support device architecture. After performing activities minimize the app. UserExperior will upload the data, which could be seen within 2-3 minutes on the UserExperior portal.`


And that's it!

The UserExperior.framework is automagically added as a target dependency, linked framework and embedded framework in a copy files build phase which is all you need to build on the simulator and a device.

### Customizing UserExperior with Key APIs:

#### 1. Add User Identifier

UserExperior SDK by default takes device id as user identifier. However, you can specify any unique user identifier of your choice (eg. Email Id, Phone Number, etc.) as custom user identifier. This identifier will show up in UserExperior portal.

- For Objective-C
    ```
        [UserExperior setUserIdentifier:@"pass-your-user-id-here"];
    ```

- For Swift
    ```swift
        UserExperior.setUserIdentifier("pass-your-user-id-here")
    ```

#### 2. Mask Sensitive Views

UserExperior SDK by default masks all the UITextField and UITextView. If you wish to mask any other UI element in your app, you can mask it by:

```swift
    let label = UILabel() 
    label.isSecureView = true
```

NOTE : Call `isSecureView` on any UI control object which is inherited from UIView

#### 3. Control Recording

UserExperior SDK has following APIs which can be used to control the recording. The APIs stopRecording, pauseRecording, resumeRecording are optional and they should be only called when you explicitly want to override the default behavior. Basically, you can use pauseRecording and resumeRecording to bypass any user flow which you don't want UserExperior to capture


##### Stop Recording
By default, recording stops automatically once the app goes to background. However, you can stop at desired point by calling this API.

- For Objective-C
    ```
        [UserExperior stopRecording];
    ```

- For Swift
    ```swift
        UserExperior.stopRecording()
    ```

#####  Pause Recording
This API pauses the recording, you can use resumeRecording API to resume.

- For Objective-C
    ```
        [UserExperior pauseRecording];
    ```

- For Swift
    ```swift
        UserExperior.pauseRecording()
    ```

##### Resume Recording
This API resumes the recording if it is paused.

- For Objective-C
    ```
        [UserExperior resumeRecording];
    ```

- For Swift
    ```swift
        UserExperior.resumeRecording()
    ```

##### Opt-In/Opt-Out

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

#### 4. Identify Subviews

UserExperior SDK automatically detects `ViewController` and defines them as screens. However, If you have used `subviews` added in existing `ViewController`, then we recommend to use the startScreen() method. This API allows you to manually define `subviews` which will be missed during auto-capturing.

- For Objective-C
    ```
        [UserExperior startScreen:@"SCREEN_NAME"];
    ```
    eg.
    ```
        [UserExperior startScreen:@"OTPViewController"];
    ```

- For Swift
    ```
        UserExperior.startScreen("SCREEN_NAME")
    ```
    eg.
    ```
        UserExperior.startScreen("OTPViewController")
    ```

**Note:** Max screenName limit is 250 chars only

#### 5. Add Events/ Messages/ Tags

  UserExperior SDK lets you track user `events`, app `messages` of your app and `tag` sessions based on some conditions using very powerful method setCustomTag()

- For Objective-C
    ```
        [UserExperior setCustomTag:@"SCREEN_NAME" customType: UECustomType];
    ```

- For Swift
    ```
        UserExperior.setCustomTag("TAG", customType: UECustomType)
    ```

  Note: Max `customTag` limit is 250 chars only

  Using this API, you can add:

  - **Events**
    In UserExperior terms, an event is the Indication of Progress in user's session. If you want to track user events which are not auto-captured by UserExperior, use UeCustomType.EVENT in 2nd parameter.

    **Example:** "Transaction Completed", "Checkout Done", "COD Payment", "Debit Card Payment", "Login", "Check Balance", "Fund Transfer" etc.

    Note: UserExperior does auto event tracking for most of the UI elements, add only those events which UserExperior didn't auto track. (which can be known in few initial recorded sessions itself.)

    **Recommendation:** Kindly pass hard coded/fixed values for events, do not pass incremental values!

    **Example**
       - For Objective-C
            ```
                [UserExperior setCustomTag:@"TAG" customType: UECustomType.event];
            ```

       - For Swift
            ```
                UserExperior.setCustomTag("TAG", customType: UECustomType.event)
            ```

  - **Messages**
    A message can be any app message shown to user, any response or error message or toast message or validation messages or messages shown on dialog boxes etc. which indicates a response to the user by the app. To add message, use UeCustomType.MSG in 2nd parameter.

    **Example:** "Please select location", "Enable location permission", "User Name or Password is incorrect", etc.

    **Example**
       - For Objective-C
            ```
                [UserExperior setCustomTag:@"TAG" customType: UECustomType.msg];
            ```
    
       - For Swift
            ```
                UserExperior.setCustomTag("TAG", customType: UECustomType.msg)
            ```

  - **Tags**

    In UserExperior terms, a tag is a kind of behaviour in the user's session. You can add Tag to even create segments of users based on behaviour or a certain condition, you can define your own tags for your app. To define your own tag, use UeCustomType.TAG in 2nd parameter.

    e.g. "Free User", "Paid User", "Burgundy User", "No Txn by User", "Free Subscription", etc.

    **Example**
       - For Objective-C
            ```
                [UserExperior setCustomTag:@"TAG" customType: UECustomType.tag];
            ```
    
       - For Swift
            ```
                UserExperior.setCustomTag("TAG", customType: UECustomType.tag)
            ```


#### 6. Track Response Time of Methods/ API Calls

UserExperior SDK allows you to track the load/ response time of the components in your app using method called `startTimer` and `stopTimer`. You can call `startTimer` method at any event on the app from which you want to track the load/ response time and call a `stopTimer` method at the event completion. This method will calculate the complete response time.

- For Objective-C
    ```
        [UserExperior startTimer:@"TIMER_NAME"];
        [UserExperior stopTimer:@"TIMER_NAME"];
    ```

- For Swift
    ```
        UserExperior.startScreen("TIMER_NAME")
        UserExperior.stopTimer("TIMER_NAME")
    ```
    
**e.g.** Suppose, you have a `TableView` on your screen which gets loaded with data you receive from the server. You can call `startTimer` method when view resumes to the user and call `stopTimer` method when data gets successfully shown in the `TableView`. Now, you can know how much time it takes to load data after screen is visible to the user. Similarly, you can use `startTimer` at any method call and `endTimer` on method response.

**Example:**
- For Objective-C
    -  While data loading starts in TableView:
        ```
            [UserExperior startTimer:@"Table view laoding timer"]; 
        ``` 
        
    -  While data loaded completed in TableView :
        ```
            [UserExperior stopTimer:@"Table view laoding timer"];
        ```

- For Swift
    -  While data loading starts in TableView:
        ```
            UserExperior.startScreen("Table view laoding timer") 
        ``` 
        
    -  While data loaded completed in TableView :
        ```
            UserExperior.stopTimer("Table view laoding timer")
        ```

   
 **Note:** Max `timerName` limit is 250 chars only


#### 7. User Consent before recording 

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

### FAQs

#### `Important` - App transport security setting

If you are using Xcode 8.0 and Swift 3.0 or Swift 2.2 or even Objective C then add this in the plist:

```
<key>App Transport Security Settings</key>
<dict>
     <key>Allow Arbitrary Loads</key><true/>
</dict>
```

#### What is NSAllowsArbitraryLoads? 
A Boolean value used to disable App Transport Security for any domains not listed in the NSExceptionDomains dictionary. Listed domains use the settings specified for that domain. The default value of NO requires the default App Transport Security behaviour for all connections.

More reference:

- [Stackoverflow](https://stackoverflow.com/questions/31254725/transport-security-has-blocked-a-cleartext-http)

