# ReactNative

## Integration

### 1. Install & Link UserExperior Plugin
   - **Install**

        ```
        npm install --save react-native-userexperior@latest
        ```
   - **Link**

        ```
        react-native link react-native-userexperior
        ```

### 2. Start UserExperior Plugin
 ```
      var UserExperior = require('react-native-userexperior');
      UserExperior.startRecording("your-version-key-here");
```
   Call the above method when your app starts (when your root component loads)
  
    
### 3. Platform specific configuration (Android & iOS) 

#### Android
- **Proguard Rules**

  If you are using Proguard in your project, you must add the following lines to your configuration:

    ```
      -dontwarn com.userexperior.**  
      -keep class com.userexperior.** { *; }
    ```

#### iOS
#####   **Automatic Integration**

Add the header path in `react-native-userExperior` (Only in case of React native version 0.60.0 and higher )
1. Open the xcode project (.xcworkspace) & click on pod (As shown in image)
2. Click on `react-native-userexperior`
3. Go to build setting and search for `Header search paths`
4. Add following path under expanded list of `Header search path`

    ```
      ${PODS_ROOT}/UserExperior/UserExperior.framework/Headers/
    ```

    ![](https://i.ibb.co/JHRxhfj/Screenshot-2020-06-01-at-18-59-35.png)

-     ` Note: Now the integration is completed, build the app. Install app and test it on REAL DEVICES ONLY. After performing activities minimize the app. UserExperior will upload the data, which could be seen within 2-3 minutes on the UserExperior portal.`
-     `Recommendation: Use Xcode v11.4 or above`

##### **Manual Integration**
   1. In XCode, in the project navigator, right click `Libraries` ➜ `Add Files to [your project's name]`
   2. Go to `node_modules` ➜ `react-native-user-experior` and add `RNUserExperior.xcodeproj`
   3. Click `RNUserExperior.xcodeproj` in the project navigator and go the Build Settings tab. Make sure `All` is toggled on (instead of 'Basic'). Look for Header Search Paths and make sure it contains both `$(SRCROOT)/../react-native/React` and `$(SRCROOT)/../../React`, mark both as recursive.
   4. Download `UserExperior.Framework` from [LINK](https://userexperior-e174e.firebaseapp.com/download/ios_sdk/4.4.5/UserExperior.zip) and add it in the Project folder.
   5. Add the header path in `RNUserExperior.xcodeproj` ➜ `Build Settings` -> `header search path`
        ```
          $[PATH TO FRAMEWORK]/UserExperior.framework/Headers/
         ```
   6. Run your project (`Cmd+R`)<



## Customizing UserExperior with Key APIs

### 1. Add User Identifier

  UserExperior SDK by default takes device id as user identifier. However, you can specify any unique user identifier of your choice (eg. Email Id, Phone Number, etc.) as custom user identifier. This identifier will show up in UserExperior portal.

  ```
  void setUserIdentifier(String userIdentifier)
  ```

  Note: Max `userIdentifier` limit is 250 chars only

  Code Example:

  ```
  UserExperior.setUserIdentifier(“pass-your-user-id-here”);
  ```

### 2. **Add Events/Messages/Tags**

  UserExperior SDK lets you track user events, app responses/messages of your app and tag sessions based on some conditions using very powerful API called setCustomTag.

  ```
  void setCustomTag(String customTag, String customType)
  ```

  Note: Max `customTag` limit is 250 chars only

  Using this API, you can add:

  - **Events**

    In UserExperior terms, an event is the Indication of Progress in user's session. If you want to track user events which are not auto-captured by UserExperior, use **"EVENT"** in 2nd parameter.

    e.g. "Txn Completed", "Checkout Done", "COD Payment", "Debit Card Payment", "Login", "Check Balance", "Fund Transfer" etc.

    Note: UserExperior does auto event tracking for most of the UI elements, add only those events which UserExperior didn't auto track. (which can be known in few initial recorded sessions itself.)

    **Recommendation:** Kindly pass hardcoded/fixed values for events, do not pass incremental values!

    Code Example:

    ```
    UserExperior.setCustomTag("Mobile Top-up",  "EVENT");
    ```

  - **Messages**

    A message can be any app message shown to user, any response or error message or toast message or validation messages or messages shown on dialog boxes etc. which indicates a response to the user by the app. To add message, use **"MSG"** in 2nd parameter.

    e.g. "Please select location", "Enable location permission", "User Name or Password is incorrect", etc.

    Code Example:

    ```
    UserExperior.setCustomTag("Please select location!", "MSG");
    ```

  - **Tags**

    In UserExperior terms, a tag is a kind of behaviour in the user's session. You can add Tag to even create segments of users based on behaviour or a certain condition, you can define your own tags for your app. To define your own tag, use **"TAG"** in 2nd parameter.

    e.g. "Free User", "Paid User", "Burgundy User", "No Txn by User", "Free Subscription", etc.

    Code Example:

    ```
    UserExperior.setCustomTag("Free User", "TAG");
    ```

### 3. **Control Recording**

  UserExperior SDK has following APIs which can be used to control the recording. The APIs stopRecording, pauseRecording, resumeRecording are optional and they should be only called when you explicitly want to override the default behavior. Basically, you can use pauseRecording and resumeRecording to bypass any user flow which you don't want UserExperior to capture.

  ```
  void stopRecording()
  ```

  By default, recording stops automatically once the app goes to background. However, you can stop at desired point by calling this API.

  ```
  void pauseRecording()
  ```

  This API pauses the recording, you can use resumeRecording API to resume.

  ```
  void resumeRecording()
  ```

  This API resumes the recording if it is paused.

### 4. **Opt-out/Opt-in**

UserExperior by default opts-in users for session recording. If you want to enable or disable recording, you can use our APIs optIn()/optOut():

  ```
  void optOut()
  ```
  
This method stops and deletes the current session recording and also disables the session recording by our sdk for this user in future.
  
  ```
  void optIn()
  ```
  
SDK by default opts-in users for session recording on app installs. If the user was disabled for session recording by using the optOut() method, you can use this method to enable recording at runtime.

  ```
  boolean getOptOutStatus()
  ```

This method returns the status of the user whether user is currently opted-in or opted-out. Boolean value true indicates that user is opted-out and false indicates that user is opted-in.

User recording resets to opt-in if the user un-installs and re-installs the app.

### 5. **User Consent before recording**

As per GDPR guidelines, we have implemented a new feature called User Consent. This feature enables you to take consent from user before starting the session recording of that user. This will show a popup to the user on app launch, asking permission to track users app screen, gestures, in-app activities. If the user does not provide a consent then that users session and users details will not be recorded in the future.

We recommend user consent to be taken on app launch, after starting UserExperior SDK you can make call to consent API:

  ```
  void consent()
  ```

## FAQs

##### **When can we see the videos of the user's session?**

When the app is minimised to the background then UserExperior SDK processes the session captured and send the information to UserExperior server.

##### **How long does it take for the video session to appear on the dashboard?**

From the time the app is minimised to the background the session captured will take 5 to 7 minutes to be reflected on UserExperior dashboard.

##### **Will the session upload if I kill the app?**

If the app is killed without minimising the app to the background, then the session which was killed will not get uploaded. UserExperior will be able to send the data whenever the app is minimised to the background.

##### **What if the user does not have network on the mobile device? Will the video get captured?**

If the user does not have an active internet on their device at the time of start of session or during the end while uploading, then UserExperior stores the session locally in the apps secure memory. This stored session is sent to the UserExperior server when the users access the app again with an active internet.

##### **Does UserExperior Track events?**

Yes, By default UserExperior tracks native events. But if you want to track events done on custom controls you can track these events by calling a Customtag event.

##### **Can I add my own custom event, like we do for other SDK's?**

Yes you can add custom events using Customtag API.

**Can I uniquely identify users session on the dashboard?**

Yes, use SetUserIdentifier API.

##### **We use fragments in our app, does UserExperior also detect fragments?**

Yes, user StartScreen API for fragments. This will allow UserExperior to recognise fragment as a screen.

##### **Can UserExperior also work on Cordova/Phone gap kind of frameworks?**

Yes

##### **I am getting a crash which has the following UserExperior entry in the trace `com.userexperior.*.dispatchTouchEvent` ?**

UserExperior intercepts and log every touch gesture that is occurring within the app, then dispatch it back to the original implementation. The DispatchTouchEvent/ DispatchkeyEvent class is the class that is responsible for this behaviour. The reason you see UserExperior in the stack-trace is that the UserExperior SDK was active (had a running thread) during the crash, but it did not cause the app to crash.

You can see the full list of Android methods that could be in the stack-trace here: <https://developer.android.com/reference/android/view/Window.Callback.html>

## Additional Notes

### iOS

Due to our implementation of UserExperior framework in Swift 5, Please follow below points for your react native iOS project successful build:

- Need Xcode version 10.2
- Add below line in Library Search Path of your react native project target (In Build Settings):
    ```    
    $(TOOLCHAIN_DIR)/usr/lib/swift/$(PLATFORM_NAME) 
    ```
- Add below line in the Runpath Search Path of your react native project target (In Build Settings):
    ```
    /usr/lib/swift
    ```

### Android
UserExperior SDK also writes some useful logs in the Android Studio IDE during runtime. These logs should be first point of investigation for any issue you may be facing. Known issues and workarounds:

1. In case you are getting NoClassDefFoundError, try these steps:

  1.1\. Delete build folder of your project, clean project, Run project.

  1.2\. Exit Android Studio and Re-launch it

  1.3\. Enable MultiDex in build.gradle for API level >= 21

  1.4\. Compile `com.android.support:multidex:1.0.0` in build.gradle dependencies for API level < 21 (check this [link)](https://developer.android.com/studio/build/multidex.html) and add following code in your BaseApplication

  ```
  public void onCreate(Bundle arguments) { 
      MultiDex.install(getTargetContext()); super.onCreate(arguments);
      ...
  }
  ```

  1.5\. Check if any dependency library is conflicting between UserExperior SDK and your app.

2. If you are getting 'Access to the dex task is now impossible, starting with 1.4.0', please refer to [this post.](http://stackoverflow.com/questions/34625267/access-to-the-dex-task-is-now-impossible-starting-with-1-4-0)

3. In case OutOfMemoryError please add following in `<application>` tag

  ```
  android:[largeHeap]="true"
  ```
