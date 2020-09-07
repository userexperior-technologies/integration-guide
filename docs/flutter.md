## Integration

> **Note:** Perform testing only on Real devices.

### 1. Add UserExperior to your flutter app dependencies inside pubspec.yaml

   ```
    dependencies:
      user_experior: ^1.1.13
   ```

### 2. Install UserExperior

   You can install it from the command line:

   ```
    flutter pub get
   ```

   Alternatively, your editor might support `flutter pub get`. Check the docs for your editor to learn more.

### 3. Import and Start UserExperior

   Inside your dart file import user_experior package like this:

   ```
    import 'package:user_experior/user_experior.dart';
   ```

   Then inside the first method that gets called add the following code snippet, most likely inside the class of lib/main.dart file that's getting called by this void main() => runApp(MyApp()); where MyApp is the name of your class.

   ```
    UserExperior.startRecording("put-your-version-key-here");
   ```

   Example:

   ```
    @override
    Widget build(BuildContext context) {
        UserExperior.startRecording("put-your-version-key-here");
        .....
        .....
        .....
    }
   ```

-   Note

    `Now the integration is completed, build the apk. Install apk in your android device and use the application. After performing activities minimize the app. UserExperior will upload the data, which could be seen within 2-3 minutes on the UserExperior portal.`

-   Proguard Rules

    If you are using Proguard in your project, you must add the following lines to your configuration:

    ```
    -dontwarn com.userexperior.**
    -keep class com.userexperior.** { *; }
    ```

## Customizing UserExperior with Key APIs

### 1. Add User Identifier

   UserExperior SDK by default takes device id as user identifier. However, you can specify any unique user identifier of your choice (eg. Email Id, Phone Number, etc.) as custom user identifier. This identifier will show up in the UserExperior portal.

   ```
    void setUserIdentifier(String userIdentifier)
   ```

   Note: Max `userIdentifier` limit is 250 chars only

   Code Example:

   ```
    UserExperior.setUserIdentifier("pass-your-user-id-here");
   ```

### 2. Add Events/ Messages/ Tags

   UserExperior SDK lets you track user events, app responses/messages of your app, and tag sessions based on some conditions using a very powerful API called setCustomTag.

   ```
    void setCustomTag(String customTag, String customType)
   ```

   Note: Max `customTag` limit is 250 chars only

   Using this API, you can add:

-   **Events**

    In UserExperior terms, an event is the Indication of Progress in the user's session. If you want to track user events that are not auto-captured by UserExperior, use "EVENT" in 2nd parameter.

       Eg: `Transaction Completed`, `Checkout Done`, `COD Payment`, `Debit Card Payment`, `Login`, `Check Balance`, `Fund Transfer`, etc.
    Note: UserExperior does auto event tracking for most of the UI elements, add only those events which UserExperior didn't auto track. (which can be known in few initially recorded sessions itself.)

    Recommendation: Kindly pass hardcoded/fixed values for events, do not pass incremental values!

    Code Example:

    ```
    UserExperior.setCustomTag("Mobile Top-up",  "EVENT");
    ```

-   **Messages**

    A message can be any app message shown to the user, any response or error message or toast message or validation messages or messages shown on dialog boxes, etc. which indicates a response to the user by the app. To add a message, use "MSG" in the 2nd parameter.

       Eg: `Please select location`, `Enable location permission`, `User Name or Password is incorrect`, etc.
    Code Example:

    ```
    UserExperior.setCustomTag("Please select location!", "MSG");
    ```

-   **Tags**

    In UserExperior terms, a tag is a kind of behavior in the user's session. You can add Tag to even create segments of users based on behavior or a certain condition, you can define your own tags for your app. To define your own tag, use "TAG" in 2nd parameter.

       Eg: `Free User`, `Paid User`, `Burgundy User`, `No Txn by User`, `Free Subscription`, etc.
    Code Example:

    ```
    UserExperior.setCustomTag("Free User", "TAG");
    ```

### 3. Identify Screens

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

### 4. Control Recording

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

### 5. Sleep Mode

   UserExperior SDK can be configured to go into sleep mode when the user has the app opened in the device, however not actively using it for a certain duration. e.g. map-based navigation apps, video player apps, etc.

   If UserExperior SDK is in sleep mode, any user interaction with the app awakes the SDK and the recording resumes.

   This allows having optimal recording (and thus optimal use of network resources) while still capturing user events as and when they occur.

   Sleep Mode Time (in seconds) is the duration for which SDK will wait after the last occurred user gesture to go into sleep mode.

   If Sleep Mode Time value is 0 or negative, there will be no such idle time thus no sleep mode and recording will be for the whole duration.

   You can add following meta-data under application tag of your app's AndroidManifest.xml:

   ```
    <meta-data
       android:name="com.userexperior.ueSleepModeTimeInSeconds"
       android:value="5"/>
   ```

### 6. Opt-out/Opt-in

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

### 7. User Consent before recording

As per GDPR guidelines, we have implemented a new feature called User Consent. This feature enables you to take consent from the user before starting the session recording of that user. This will show a popup to the user on the app launch, asking permission to track the user's app screen, gestures, in-app activities. If the user does not provide consent then that user session and user details will not be recorded in the future.

We recommend user consent to be taken on app launch, after starting UserExperior SDK you can make a call to consent API:

```
void consent()
```

## FAQs

**When can we see the videos of the user's session?**

When the app is minimized to the background then UserExperior SDK processes the session captured and sends the information to the UserExperior server.

**How long does it take for the video session to appear on the dashboard?**

From the time the app is minimized to the background the session captured will take 5 to 7 minutes to be reflected on UserExperior dashboard.

**Will the session upload if I kill the app?**

If the app is killed without minimizing the app to the background, then the session which was killed will not get uploaded. UserExperior will be able to send the data whenever the app is minimized to the background.

**What if the user does not have a network on the mobile device? Will the video get captured?**

If the user does not have an active internet on their device at the time of the start of the session or during the end while uploading, then UserExperior stores the session locally in the apps secure memory. This stored session is sent to the UserExperior server when the users access the app again with an active internet.

**Does UserExperior Track events?**

Yes, By default UserExperior tracks native events. But if you want to track events done on custom controls you can track these events by calling a `Customtag` event.

**Can I add my own custom event, as we do for other SDK's?**

Yes, you can add custom events using `Customtag` API.

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

UserExperior SDK also writes some useful logs in the Android Studio IDE during runtime. These logs should be the first point of investigation for any issue you may be facing. Known issues and workarounds:

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
