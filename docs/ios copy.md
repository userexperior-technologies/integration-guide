
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
        [UserExperior setUserProperties:@{@"key":@value, ...}];
    ```
    
    Eg.
    ```
        [UserExperior setUserProperties:@{@"name":@"Sam", @"phone":@9876543210}];
    ```


-   For Swift

    ```
        UserExperior.setUserProperties(["key":"value", ...])
    ```
    
    Eg.
    ```
        UserExperior.setUserProperties(["name":"Sam", "phone": 9876543210])
     ```

### 2. Log Event

UserExperior SDK lets you log user events based on the scenario. An event is the indication of Progress in the user's session. LogEvent() can be used as follows

#### a. Log event with name

-   For Objective-C

    ```
        [UserExperior logEvent:@"EVENT_GOES_HERE"];        
    ```
    
    Eg.
    ```
        [UserExperior logEvent:@"Onboarding successful!"];        
    ```


-   For Swift

    ```
        UserExperior.logEvent("EVENT_GOES_HERE")
    ```
    
    Eg.
    ```
        UserExperior.logEvent("Onboarding successful!")
    ```

    Note: Max `eventName` limit is 250 chars only
    
#### b. Log event with name and properties

-   For Objective-C

    ```
        [UserExperior logEvent:@"EVENT_GOES_HERE" properties:@{@"key":@value, ...}];        
    ```
    
    Eg,
    ```
        [UserExperior logEvent:@"Health Profile created" properties:@{@"age":@35, @"weight":@70.5}];        
    ```

-   For Swift

    ```
        UserExperior.logEvent("EVENT_GOES_HERE", properties:["key:"value", ...])
    ```
    
    Eg.
    ```
        UserExperior.logEvent("Health Profile created", properties:["age":35, "weight":70.5])
    ```

    Note: Max `eventName` limit is 250 chars only

    
### 3. Log Message

UserExperior SDK lets you log user meessage based on the scenario. A message can be any app message shown to the user, any response OR error message OR toast message OR validation messages OR messages shown on dialog boxes, etc. which indicates a response to the user by the app. LogMessage() can be used as follows

#### a. Log message with name

-   For Objective-C

    ```
        [UserExperior logEvent:@"MESSAGE_GOES_HERE"];        
    ```
    
    Eg.
    ```
        [UserExperior logEvent:@"User Name or Password is incorrect"];        
    ```

-   For Swift

    ```
        UserExperior.logEvent("MESSAGE_GOES_HERE")
    ```
    
    Eg.
    ```
        UserExperior.logEvent("User Name or Password is incorrect")
    ```

    Note: Max `messageName` limit is 250 chars only
    
#### b. Log message with name and properties

-   For Objective-C

    ```
        [UserExperior logMessage:@"MESSAGE_GOES_HERE" properties:@{@"key":@value, ...}];        
    ```
    
    Eg.
    ```
        [UserExperior logMessage:@"Login Error" properties:@{@"status_code":@400, 
                                                             @"response_message":@"invalid credentials"}];        
    ```

-   For Swift

    ```
        UserExperior.logMessage("MESSAGE_GOES_HERE", properties:["key:"value", ...])
    ```
    
    Eg.
    ```
        UserExperior.logMessage("Login Error", properties:["status_code:400, 
                                                           "response_message":"invalid credentials"])
    ```
    

   