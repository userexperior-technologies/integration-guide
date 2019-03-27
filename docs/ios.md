# Native iOS

## Integration

You can install the UserExperior iOS SDK through [cocoapods](https://cocoapods.org/) or manually.

**Via Cocoapods**

1. Install [cocoapods](https://cocoapods.org/) if you don't already have it.
2. Add to the pod file

  ```
  pod 'UserExperior', '4.0.1'
  ```

3. From your terminal, type

  - `pod repo update` (Optional - mostly if you are facing [Unable to find a specification in CocoaPods](https://stackoverflow.com/questions/25913733/unable-to-find-a-specification-in-cocoapods) issue)

    After repo update perform below command to install pod

  - `pod install`

4. Set `Always Embed Swift Standard Libraries` to `Yes` in Build Setting panel of project as well as app target. (Specially if your project based on old objective c project)

**Via Manual**

1. Follow below link to download

  - [Download](https://userexperior-35559.firebaseapp.com/download/ios_sdk/4.0.1/UserExperior.zip)

1. Unzip the file and drag the UserExperior.framework directory to the "Frameworks" in your XCode project tree.
2. In your xcode project, select your application project in the Project Navigator (blue project icon) to navigate to the target configuration window and select the application target under the `Targets` heading in the sidebar.
3. In the tab bar at the top of that window, open the `General` panel.
4. Click on the + button under the `Embedded Binaries` section.
5. You will see UserExperior.framework nested inside a `Frameworks`.
6. Select the UserExperior.framework and click `Add`.
7. Set `Always Embed Swift Standard Libraries` to `Yes` in Build Setting panel of project as well as app target. (Specially if your project based on old objective c project)

And that's it!

The UserExperior.framework is automagically added as a target dependency, linked framework and embedded framework in a copy files build phase which is all you need to build on the simulator and a device.

**After SDK Integration (Via cocoapods or manual)**

1. In your app delegate, include:

  - For Objective-C

    `#import <UserExperior/UserExperior-Swift.h>`

  - For Swift

    `#import UserExperior`

2. Add this call as the first line of your `application:didFinishLaunchingWithOptions:` method.

  - For Objective-C

    `[UserExperior initialize:@"USER_KEY"];`

  - For Swift

    `UserExperior.initialize("USER_KEY")`
