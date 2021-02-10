## Integration

**Note**:
-  Perform testing only on Real devices.
-  UserExperior supports os versions from iOS 8+!
- You can install the UserExperior iOS SDK through [CocoaPods](https://cocoapods.org/) (Install if you don't already have it) OR manually.

### Via Cocoapods

1.  Add to the pod file

For Swift 5.3.1

```
pod 'UserExperior', '4.4.39'

```

For Swift 5.3

```
pod 'UserExperior', '4.4.38'

```

For Swift 5.2

```
pod 'UserExperior', '4.4.37'

```

For Swift 5.1

```
 pod 'UserExperior', '4.4.36'

```

For Swift 5.0 & below

```
pod 'UserExperior', '4.4.35'

```

2.  From your terminal, type

    After the repo update perform the below command to install pod

    ```
    pod install

    ```
3. In your app delegate, include:

- 3. a. For Objective-C

            #import <UserExperior/UserExperior-Swift.h>

-  3. b. For Swift

            import UserExperior

4. Add this call as the first line of your `application:didFinishLaunchingWithOptions:` method.

- 4. a. For Objective-C

            [UserExperior initialize:@"USER_KEY"];

      **Note:**

      `Now the integration is completed, build the ONLY on REAL iOS DEVICES since framework support device architecture. After performing activities minimize the app. UserExperior will upload the data, which could be seen within 2-3 minutes on the UserExperior portal.`

- 4. b. For Swift

            UserExperior.initialize("USER_KEY")

        **Note:**

      `Now the integration is completed, build the ONLY on REAL iOS DEVICES since framework support device architecture. After performing activities minimize the app. UserExperior will upload the data, which could be seen within 2-3 minutes on the UserExperior portal.`


### Via Manual

1. Follow the below link to download
- [Download (For Swift 5.3.1)](https://userexperior-e174e.firebaseapp.com/download/ios_sdk/4.4.39/UserExperior.zip)
- [Download (For Swift 5.3)](https://userexperior-e174e.firebaseapp.com/download/ios_sdk/4.4.38/UserExperior.zip)
- [Download (For Swift 5.2)](https://userexperior-e174e.firebaseapp.com/download/ios_sdk/4.4.37/UserExperior.zip)
- [Download (For Swift 5.1)](https://userexperior-e174e.firebaseapp.com/download/ios_sdk/4.4.36/UserExperior.zip)
- [Download (For Swift 5.0 & Below)](https://userexperior-e174e.firebaseapp.com/download/ios_sdk/4.4.35/UserExperior.zip)

2. Unzip the file and drag the UserExperior.framework directory to the “Frameworks” in your XCode project tree.
3. In your Xcode project, select your application project in the Project Navigator (blue project icon) to navigate to the target configuration window and select the application target under the `Targets` heading in the sidebar.
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

        **Note:**

      `Now the integration is completed, build the ONLY on REAL iOS DEVICES since framework support device architecture. After performing activities minimize the app. UserExperior will upload the data, which could be seen within 2-3 minutes on the UserExperior portal.`

- 9. b. For Swift

            UserExperior.initialize("USER_KEY")

        **Note:**

      `Now the integration is completed, build the ONLY on REAL iOS DEVICES since framework support device architecture. After performing activities minimize the app. UserExperior will upload the data, which could be seen within 2-3 minutes on the UserExperior portal.`


And that's it!

The UserExperior.framework is automagically added as a target dependency, linked framework and embedded framework in a copy files build phase which is all you need to build on the simulator and a device.




## Customizing UserExperior with Key APIs:

### 1. Set User Identifier & additional properties

#### a. Set User Identifier

UserExperior SDK by default takes device id as a user identifier. However, you can specify any unique user identifier of your choice (eg. Email Id, Phone Number, etc.) as a custom user identifier. This identifier will show up in the UserExperior portal.

-   For Objective-C

    ```
        [UserExperior setUserIdentifier:@"pass-your-user-id-here"];
    ```

    Eg.
    ```
        [UserExperior setUserIdentifier:@"abc@xyz.com"];
    ```


-   For Swift

    ```
        UserExperior.setUserIdentifier("pass-your-user-id-here")
    ```

    Eg.
    ```
        [UserExperior setUserIdentifier:"abc@xyz.com"];
    ```


#### b. Send additional user information

-   For Objective-C

    ```
        [UserExperior setUserProperties:@{@"key1":@value1,
                                          @"key2":@value2, ...}];
    ```

    Eg.
    ```
        [UserExperior setUserProperties:@{@"start_date":@"2020/11/25", // Date Format YYYY/MM/DD
                                          @"plan_subscribed":@trial];    
    ```
    Note: Please send the Date in "YYYY/MM/DD" format.

-   For Swift

    ```
        UserExperior.setUserProperties(["key1:"value1",
                                        "key2:"value2", ...])
    ```

    Eg.
    ```
        UserExperior.setUserProperties(["start_date": "2020/12/31", // Date-Format: YYYY/MM/DD
                                         "plan_subscribed": "trial"])
    ```
    Note: Please send the Date property in "YYYY/MM/DD" format only.

### 2. Log Event

UserExperior SDK lets you log user events based on the scenario. An event is the indication of Progress in the user's session. LogEvent() can be used as follows

#### a. Log event with name

-   For Objective-C

    ```
        [UserExperior logEvent:@"YOUR_EVENT"];        
    ```

    Eg.
    ```
        [UserExperior logEvent:@"Onboarding successful!"];        
    ```


-   For Swift

    ```
        UserExperior.logEvent("YOUR_EVENT")
    ```

    Eg.
    ```
        UserExperior.logEvent("Onboarding successful!")
    ```

    Note: Max `eventName` limit is 250 chars only.

#### b. Log event with name and properties

-   For Objective-C

    ```
        [UserExperior logEvent:@"YOUR_EVENT" properties:@{@"key1":@value1,
                                                          @"key2":@value2, ...}];        
    ```

    Eg,
    ```
        [UserExperior logEvent:@"Health Profile created" properties:@{@"age":@35,
                                                                      @"weight":@70.5}];        
    ```

-   For Swift

    ```
        UserExperior.logEvent("YOUR_EVENT", properties:["key1:"value1",
                                                        "key2:"value2", ...])
    ```

    Eg.
    ```
        UserExperior.logEvent("Health Profile created", properties:["age":35,
                                                                    "weight":70.5])
    ```

    Note:
    - Max `eventName` limit is 250 chars only.
    - Please send the Date property in "YYYY/MM/DD" format only.

### 3. Log Message

UserExperior SDK lets you log user message based on the scenario. A message can be any app message shown to the user, any response OR error message OR toast message OR validation messages OR messages shown on dialog boxes, etc. which indicates a response to the user by the app. LogMessage() can be used as follows

#### a. Log message with name

-   For Objective-C

    ```
        [UserExperior logMessage:@"YOUR_MESSAGE"];        
    ```

    Eg.
    ```
        [UserExperior logMessage:@"User Name or Password is incorrect"];        
    ```

-   For Swift

    ```
        UserExperior.logMessage("YOUR_MESSAGE")
    ```

    Eg.
    ```
        UserExperior.logMessage("User Name or Password is incorrect")
    ```

    Note: Max `messageName` limit is 250 chars only.

#### b. Log message with name and properties

-   For Objective-C

    ```
        [UserExperior logMessage:@"YOUR_MESSAGE" properties:@{@"key1":@value1,
                                                              @"key2":@value2, ...}];        
    ```

    Eg.
    ```
        [UserExperior logMessage:@"Login Error" properties:@{@"status_code":@400,
                                                             @"response_message":@"invalid credentials"}];        
    ```

-   For Swift

    ```
        UserExperior.logMessage("YOUR_MESSAGE", properties:["key1:"value1",
                                                            "key2:"value2", ...])
    ```

    Eg.
    ```
        UserExperior.logMessage("Login Error", properties:["status_code:400,
                                                           "response_message":"invalid credentials"])
    ```

    Note:
    - Max `messageName` limit is 250 chars only.
    - Please send the Date property in "YYYY/MM/DD" format only.


### 4. Mask Sensitive Views

UserExperior SDK by default masks all the UITextField and UITextView. If you wish to mask any other UI element in your app, you can mask it by:

```
    let label = UILabel()
    label.isSecureView = true
```

NOTE : Call `isSecureView` on any UI control object which is inherited from UIView


### 5. Identify Screens

UserExperior SDK automatically detects `ViewController` and defines them as screens. However, If you have used `subviews` added in the existing `ViewController`, then we recommend to use the `startScreen()` method. This API allows you to manually define `subviews` which will be missed during auto-capturing.

-   For Objective-C

    ```
        [UserExperior startScreen:@"SCREEN_NAME"];
    ```

    Eg.

    ```
        [UserExperior startScreen:@"OTPViewController"];
    ```

-   For Swift

    ```
        UserExperior.startScreen("SCREEN_NAME")
    ```

    Eg.

    ```
        UserExperior.startScreen("OTPViewController")
    ```

Note: Max screenName limit is 250 chars only


### 6. Track Response Time of Methods/ API Calls

UserExperior SDK allows you to track the load/ response time of the components in your app using a method called `startTimer` and `stopTimer`. You can call `startTimer` method at any event on the app from which you want to track the load/ response time and call a `stopTimer` method at the event completion. This method will calculate the complete response time.

-   For Objective-C

    ```
        [UserExperior startTimer:@"TIMER_NAME"];
        [UserExperior stopTimer:@"TIMER_NAME"];
    ```

-   For Swift

    ```
        UserExperior.startTimer("TIMER_NAME")
        UserExperior.stopTimer("TIMER_NAME")
    ```

Eg: Suppose, you have a `TableView` on your screen which gets loaded with data you receive from the server. You can call `startTimer` method when view resumes to the user and call `stopTimer` method when data gets successfully shown in `TableView`. Now, you can know how much time it takes to load data after the screen is visible to the user. Similarly, you can use `startTimer` at any method call and `endTimer` on method response.

Example:

-   For Objective-C

    -   While data loading starts in TableView:

        ```
            [UserExperior startTimer:@"Load Money API call"];
        ```

    -   While data loaded completed in TableView :

        ```
            [UserExperior stopTimer:@"Load Money API call"];
        ```

-   For Swift

    -   While data loading starts in TableView:

        ```
            UserExperior.startTimer("Load Money API call")
        ```

    -   While data loaded completed in TableView :

        ```
            UserExperior.stopTimer("Load Money API call")
        ```

    Note: Max `timerName` limit is 250 chars only


### 7. Control Recording

UserExperior SDK has the following APIs which can be used to control the recording. The APIs `stopRecording`, `pauseRecording`, `resumeRecording` are optional and they should be only called when you explicitly want to override the default behavior. Basically, you can use `pauseRecording` and `resumeRecording` to bypass any user flow which you don't want UserExperior to capture

**Stop Recording:**
By default, recording stops automatically once the app goes to the background. However, you can stop at the desired point by calling this API.

-   For Objective-C

    ```
        [UserExperior stopRecording];
    ```

-   For Swift

    ```
        UserExperior.stopRecording()
    ```

**Pause Recording:**
 This API pauses the recording, you can use `resumeRecording` API to resume.

-   For Objective-C

    ```
        [UserExperior pauseRecording];
    ```

-   For Swift

    ```
        UserExperior.pauseRecording()
    ```

**Resume Recording:**
 This API resumes the recording if it is paused.

-   For Objective-C

    ```
        [UserExperior resumeRecording];
    ```

-   For Swift

    ```
        UserExperior.resumeRecording()
    ```

### 8. Opt-In/Opt-Out

SDK by default opts-in users for session recording on app installs. If the user was disabled for session recording by using the `optOut()` method, you can use this method to enable recording at runtime.

-   For Objective-C

    ```
        [UserExperior optIn];
    ```

-   For Swift

    ```
        UserExperior.optIn()
    ```

This method returns the status of the user whether the user is currently opted-in or opted-out. The boolean value true indicates that the user is opted-out and false indicates that the user is opted-in.

-   For Objective-C

    ```
        [UserExperior getOptOutStatus];
    ```

-   For Swift

    ```
        UserExperior.getOptOutStatus()
    ```

## What is NSAllowsArbitraryLoads?

A Boolean value used to disable App Transport Security for any domains not listed in the NSExceptionDomains dictionary. Listed domains use the settings specified for that domain. The default value of NO requires the default App Transport Security behavior for all connections.
