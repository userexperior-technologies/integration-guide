
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
