## Integration

> **Note**:
-  UserExperior supports os versions from Android JellyBean (4.3) API Level 16 to Android 11 API Level 30 & iOS 10 and above!
- XCode Support: 11.5 and above

### 1.  Add UserExperior Plugin to your Project

-   First, Remove UserExperior Plugin (only if it is already installed)

    For Cordova app:

    ```
    cordova plugin remove userexperior-cordova-plugin
    ```

    For Ionic-Cordova app:

    ```
    ionic cordova plugin remove userexperior-cordova-plugin
    ```

-   Add UserExperior Plugin

    For Cordova app:

    ```
    cordova plugin add userexperior-cordova-plugin
    ```

    For Ionic-Cordova app:

    ```
    ionic cordova plugin add userexperior-cordova-plugin
    ```

### 2. Start UserExperior Plugin

   ```
    UserExperior.startRecording("your-version-key-here");
   ```
   Call the above method when your app starts, preferably when the `DeviceReady` event fires.

   If you're using TypeScript (default in ionic 2 and ionic 3), put the following line under the imports:

   ```
    declare var UserExperior:any;
   ```

- **For iOS: pod install**
   Perform pod install in `../platforms/ios` directory

   ```
    pod install
   ```

-   **For Android: Proguard Rules**

    If you are using Proguard in your project, you must add the following lines to your configuration:

    ```
    -dontwarn com.userexperior.**
    -keep class com.userexperior.** { *; }
    ```

-   **Note**

    `Now the integration is completed, build the apk. Install apk in your android device and use the application. After performing activities minimize the app. UserExperior will upload the data, which could be seen within 2-3 minutes on the UserExperior portal.`


## Customizing UserExperior with Key APIs

### 1. Set User Identifier & additional properties

#### a. Set User Identifier

UserExperior SDK by default takes device id as a user identifier. However, you can specify any unique user identifier of your choice (eg. Email Id, Phone Number, etc.) as a custom user identifier. This identifier will show up in the UserExperior portal.

   Syntax:
   ```
    void setUserIdentifier(String userIdentifier)
   ```

   Eg.
  ```
    UserExperior.setUserIdentifier("abc@xyz.com");
  ```
  Note: Max `userIdentifier` limit is 250 chars only

#### b. Send additional user information

   Syntax:
  ```
    UserExperior.setUserProperties({key1: value1,
                                    key2: value2, ...});
  ```
   Eg.
  ```
    UserExperior.setUserProperties({"start_date": "2020/12/31", // Date-Format: YYYY/MM/DD
                                    "plan_subscribed": "trial"});
  ```
   Note: 
   - Please send the `date property` in ``"YYYY/MM/DD"`` format only, if any.
   - Max `key` & `value` limit is 250 chars only respectively


### 2. Log Event

UserExperior SDK lets you log user events based on the scenario. An event is the indication of Progress in the user's session. LogEvent() can be used as follows

#### a. Log event with name

  Syntax:
 ```
   UserExperior.logEvent("YOUR_EVENT");
 ```
  Eg.
 ```
   UserExperior.logEvent("Registration Successful");
 ```
  Note: Max `eventName` limit is 250 chars only

#### b. Log event with name and properties

  Syntax:
 ```
  UserExperior.logEventWithProperties("YOUR_EVENT", {"key1:"value1",
                                       "key2:"value2", ...})        
 ```
  Eg.
 ```
  UserExperior.logEventWithProperties("Health Profile created", {"age":35,
                                                   "weight":70.5})        
 ```
  Note:
  - Max `eventName` limit is 250 chars only.
  - Max `key` & `value` limit is 250 chars only respectively
  - Please send the `date property` in `"YYYY/MM/DD"` format only, if any.

### 3. Log Message

UserExperior SDK lets you log user message based on the scenario. A message can be any app message shown to the user, any response OR error message OR toast message OR validation messages OR messages shown on dialog boxes, etc. which indicates a response to the user by the app. LogMessage() can be used as follows

#### a. Log message with name

  Syntax:
 ```
   UserExperior.logMessage("YOUR_MESSAGE");
 ```
  Eg.
 ```
   UserExperior.logMessage("User Name or Password is incorrect");
 ```
  Note: Max `messageName` limit is 250 chars only

#### b. Log message with name and properties

  Syntax:
 ```
  UserExperior.logMessageWithProperties("YOUR_MESSAGE", {"key1:"value1",
                                           "key2:"value2", ...})
 ```
  Eg.
 ```
  UserExperior.logMessageWithProperties("Login Error", {"status_code:400,
                                          "response_message":"invalid credentials"})
 ```
 Note:
 - Max `messageName` limit is 250 chars only.
 - Max `key` & `value` limit is 250 chars only respectively
 - Please send the `date property` in `"YYYY/MM/DD"` format only, if any.


### 4. Identify Screens

   UserExperior SDK automatically detects Activities/ViewControllers and defines them as screens. However, If you have used js or anything else to represent your screens, then we recommend using the `startScreen` API. This API allows you to manually define screens.

   ```
    void startScreen(String screenName)
   ```

   Note: Max `screenName` limit is 250 chars only

   Recommendation: Kindly pass hardcoded/fixed values for screen names, do not pass incremental values!

   Code Example:

   ```
    UserExperior.startScreen("Notification Page");
   ```

   Note: This method should be usually called when your page loads.


### 5. Track Response Time of Methods/ API Calls

   UserExperior SDK allows you to track the load/response time of the components in your app using APIs called `startTimer` and endTimer. You can call `startTimer` API at any event on the app from which you want to track the load/response time and call an `endTimer` API at the event completion. These APIs will calculate the complete response time.

   ```
    void startTimer(String timerName)
    void endTimer(String timerName)
   ```

   Note: Max `timerName` limit is 250 chars only

   Eg: Suppose, you have a ListView on your screen which gets loaded with data you receive from the server. You can call `startTimer` API when the screen resumes to the user and call `endTimer` API when data gets successfully shown in the ListView. Now you can know how much time it takes to load data after the screen is visible to the user. Similarly, you can use `startTimer` at any API call and an `endTimer` on API response.

   Code Example:

   ```
    UserExperior.startTimer("Load Money API call");
    UserExperior.endTimer("Load Money API call");
   ```

### 6. Control Recording

   UserExperior SDK has the following APIs which can be used to control the recording. The APIs `stopRecording`, `pauseRecording`, `resumeRecording` are optional and they should be only called when you explicitly want to override the default behavior. Basically, you can use `pauseRecording` and `resumeRecording` to bypass any user flow which you don't want UserExperior to capture.

   ```
    void stopRecording()
   ```

   By default, recording stops automatically once the app goes to the background. However, you can stop at the desired point by calling this API.

   ```
    void pauseRecording()
   ```

   This API pauses the recording, you can use `resumeRecording` API to resume.

   ```
    void resumeRecording()
   ```

   This API resumes the recording if it is paused.

### 7. Opt In/ Opt Out

UserExperior by default opts-in users for session recording. If you want to enable or disable recording, you can use our APIs optIn()/optOut():

```
void optOut()
```

This method stops and deletes the current session recording and also disables the session recording by our SDK for this user in the future.

```
void optIn()
```

SDK by default opts-in users for session recording on app installs. If the user was disabled for session recording by using the `optOut()` method, you can use this method to enable recording at runtime.

```
boolean getOptOutStatus()
```

This method returns the status of the user whether the user is currently opted-in or opted-out. The boolean value true indicates that the user is opted-out and false indicates that the user is opted-in.

User recording resets to opt-in if the user un-installs and re-installs the app.

## FAQs

**When can we see the videos of the user's session?**

When the app is minimized to the background then UserExperior SDK processes the session captured and sends the information to the UserExperior server.

**How long does it take for the video session to appear on the dashboard?**

From the time the app is minimized to the background the session captured will take 5 to 7 minutes to be reflected on the UserExperior dashboard.

**Will the session upload if I kill the app?**

If the app is killed without minimizing the app to the background, then the session which was killed will not get uploaded. UserExperior will be able to send the data whenever the app is minimized to the background.

**What if the user does not have a network on the mobile device? Will the video get captured?**

If the user does not have an active internet on their device at the time of the start of the session or during the end while uploading, then UserExperior stores the session locally in the apps secure memory. This stored session is sent to the UserExperior server when the users access the app again with an active internet.

**Does UserExperior Track events?**

Yes, By default UserExperior tracks native events. But if you want to track events done on custom controls you can track these events by calling a `Customtag` event.

**Can I add my own custom event, as we do for other SDK's?**

Yes you can add custom events using `Customtag` API.

**Can I uniquely identify users session on the dashboard?**

Yes, use SetUserIdentifier API.

**We use fragments in our app, does UserExperior also detect fragments?**

Yes, user `StartScreen` API for fragments. This will allow UserExperior to recognize fragment as a screen.

**Can UserExperior also work on Cordova/Phone gap kind of frameworks?**

Yes

**I am getting a crash which has the following UserExperior entry in the trace `com.userexperior.*.dispatchTouchEvent` ?**

UserExperior intercepts and logs every touch gesture that is occurring within the app, then dispatch it back to the original implementation. The DispatchTouchEvent/ DispatchkeyEvent class is the class that is responsible for this behavior. The reason you see UserExperior in the stack-trace is that the UserExperior SDK was active (had a running thread) during the crash, but it did not cause the app to crash.

You can see the full list of Android methods that could be in the stack-trace here: <https://developer.android.com/reference/android/view/Window.Callback.html>

## Additional Notes

UserExperior SDK also writes some useful logs in the Android Studio IDE during runtime. These logs should be first point of investigation for any issue you may be facing. Known issues and workarounds:

1.  In case you are getting NoClassDefFoundError, try these steps:

    1.1. Delete build folder of your project, clean project, Run project.

    1.2. Exit Android Studio and Re-launch it

    1.3. Enable MultiDex in build.gradle for API level >= 21

    1.4. Compile `com.android.support:multidex:1.0.0` in build.gradle dependencies for API level < 21 (check this [link)](https://developer.android.com/studio/build/multidex.html) and add following code in your BaseApplication

    ```
    public void onCreate(Bundle arguments) {
       MultiDex.install(getTargetContext()); super.onCreate(arguments);
       ...
    }
    ```

    1.5. Check if any dependency library is conflicting between UserExperior SDK and your app.

2.  If you are getting 'Access to the dex task is now impossible, starting with 1.4.0', please refer to [this post.](https://stackoverflow.com/questions/34625267/access-to-the-dex-task-is-now-impossible-starting-with-1-4-0)

3.  In case OutOfMemoryError please add following in `<application>` tag

    ```
    android:[largeHeap]="true"
    ```
