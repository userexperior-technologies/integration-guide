# ReactNative

## Integration

1. **Install & Link UserExperior Plugin**

  - **Install**

    ```
    npm install --save react-native-userexperior@latest
    ```

  - **Link**

    ```
    react-native link react-native-userexperior
    ```

2. **Start UserExperior Plugin**

  ```
  var UserExperior = require('react-native-userexperior');
  UserExperior.startRecording("your-version-key-here");
  ```

  Call the above method when your app starts (when your root component loads)


- **Note**

  Now the integration is completed, build the apk. Install apk in your android device and use the application. After performing activities minimize the app. UserExperior will upload the data, which could be seen within 5-7 minutes on the dashboard.

- **Proguard Rules**

  If you are using Proguard in your project, you must add the following lines to your configuration:

  ```
  -dontwarn com.userexperior.**  
  -keep class com.userexperior.** { *; }
  ```

## Customizing UserExperior with Key APIs

1. **Add User Identifier**

  UserExperior SDK by default takes device id as user identifier. However, you can specify any unique user identifier of your choice (eg. Email Id, Phone Number, etc.) as custom user identifier. This identifier will show up in UserExperior portal.

  ```
  void setUserIdentifier(String userIdentifier)
  ```

  Note: Max `userIdentifier` limit is 250 chars only

  Code Example:

  ```
  UserExperior.setUserIdentifier(“pass-your-user-id-here”);
  ```

2. **Add Events/Messages/Tags**

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

3. **Identify Screens**

  UserExperior SDK automatically detects Activities and defines them as screens. However, If you have used fragments or anything else to represent your screens, then we recommend to use the "startScreen API". This API allows you to manually define screens.

  ```
  void startScreen(String screenName)
  ```

  Note: Max `screenName` limit is 250 chars only

  **Recommendation:** Kindly pass hardcoded/fixed values for screen names, do not pass incremental values!

  Code Example:

  ```
  UserExperior.startScreen("Notification Page");
  ```

  Note: This method should be usually called when your page loads.

4. **Track Response Time of Methods/API Calls**

  UserExperior SDK allows you to track the load/response time of the components in your app using APIs called startTimer and endTimer. You can call startTimer API at any event on the app from which you want to track the load/response time and call a stopTimer API at the event completion. This APIs will calculate the complete response time.

  ```
  void startTimer(String timerName)
  void endTimer(String timerName)
  ```

  Note: Max `timerName` limit is 250 chars only

  e.g. Suppose, you have a ListView on your screen which gets loaded with data you receive from the server. You can call startTimer API when screen resumes to the user and call stopTimer API when data gets successfully shown in the ListView. Now you can know how much time it takes to load data after screen is visible to the user. Similarly, you can use startTimer at any API call and endTimer on API response.

  Code Example:

  ```
  // Call it at API call  
  UserExperior.startTimer("Load Money API call");  

  // call it at API response  
  UserExperior.endTimer("Load Money API call");
  ```

5. **Control Recording**

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

6. **Get Precise User Location**

  UserExperior SDK lets you track the location of your user. If your app has location permissions enabled and you wish to know the exact city and country of your users, you can use our API setDeviceLocation. You just have to pass us the location parameters latitude and longitude which you get from the gps location in your app and through this data, we will only present City and Country on our dashboard which can be used for further analytics.

  ```
  void setDeviceLocation(double latitude, double longitude)
  ```

  Code Example:

  ```
  // These are hardcoded lat, long, you can pass actual lat, long if your app uses gps  
  UserExperior.setDeviceLocation(19.154023, 72.945204);
  ```

7. **Sleep Mode**

  UserExperior SDK can be configured to go into sleep mode when user has the app opened in the device, however not actively using it for certain duration. e.g. map based navigation apps, video player apps, etc.

  If UserExperior SDK is in sleep mode, any user interaction with the app awakes the SDK and the recording resumes.

  This allows having optimal recording (and thus optimal use of network resources) while still capturing user events as and when they occur.

  Sleep Mode Time (in seconds) is the duration for which SDK will wait after last occurred user gesture to go into sleep mode.

  If Sleep Mode Time value is 0 or negative, there will be no such idle time thus no sleep mode and recording will be for whole duration.

  You can add following meta-data under application tag of your app's **AndroidManifest.xml**:

  ```
  <meta-data  
      android:name="com.userexperior.ueSleepModeTimeInSeconds"  
      android:value="5"/>
  ```

## FAQs

**When can we see the videos of the user's session?**

When the app is minimised to the background then UserExperior SDK processes the session captured and send the information to UserExperior server.

**How long does it take for the video session to appear on the dashboard?**

From the time the app is minimised to the background the session captured will take 5 to 7 minutes to be reflected on UserExperior dashboard.

**Will the session upload if I kill the app?**

If the app is killed without minimising the app to the background, then the session which was killed will not get uploaded. UserExperior will be able to send the data whenever the app is minimised to the background.

**What if the user does not have network on the mobile device? Will the video get captured?**

If the user does not have an active internet on their device at the time of start of session or during the end while uploading, then UserExperior stores the session locally in the apps secure memory. This stored session is sent to the UserExperior server when the users access the app again with an active internet.

**Does UserExperior Track events?**

Yes, By default UserExperior tracks native events. But if you want to track events done on custom controls you can track these events by calling a Customtag event.

**Can I add my own custom event, like we do for other SDK's?**

Yes you can add custom events using Customtag API.

**Can I uniquely identify users session on the dashboard?**

Yes, use SetUserIdentifier API.

**We use fragments in our app, does UserExperior also detect fragments?**

Yes, user StartScreen API for fragments. This will allow UserExperior to recognise fragment as a screen.

**Can UserExperior also work on Cordova/Phone gap kind of frameworks?**

Yes

**I am getting a crash which has the following UserExperior entry in the trace `com.userexperior.*.dispatchTouchEvent` ?**

UserExperior intercepts and log every touch gesture that is occurring within the app, then dispatch it back to the original implementation. The DispatchTouchEvent/ DispatchkeyEvent class is the class that is responsible for this behaviour. The reason you see UserExperior in the stack-trace is that the UserExperior SDK was active (had a running thread) during the crash, but it did not cause the app to crash.

You can see the full list of Android methods that could be in the stack-trace here: <https://developer.android.com/reference/android/view/Window.Callback.html>

## Additional Notes

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

4. If you find this log under logcat "**Unable to start service Intent { cmp=com.yourcompanydomain.yourappname/com.userexperior.services.recording.EventSession (has extras) } U=0: not found**", please add following services manually to your app's AndroidManifest.xml:

  ```
  <service  
    android:name="com.userexperior.services.UploadService"  
    android:enabled="true"  
    android:exported="false" />  

  <service  
    android:name="com.userexperior.services.recording.EventSession"  
    android:enabled="true"  
    android:exported="false">  
  </service>  

  <service  
    android:name="com.userexperior.services.recording.ScreenShotService"  
    android:enabled="true"  
    android:exported="false">  
  </service>
  ```
