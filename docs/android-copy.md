
## Customizing UserExperior with Key APIs:

### 1. Set User Identifier & additional properties

#### a. Set User Identifier

UserExperior SDK by default takes device id as a user identifier. However, you can specify any unique user identifier of your choice (eg. Email Id, Phone Number, etc.) as a custom user identifier. This identifier will show up in the UserExperior portal.

   Syntax:
    
    UserExperior.setUserIdentifier("pass-your-user-id-here");
    
    
   Eg.
    
    UserExperior.setUserIdentifier("abc@xyz.com");
    

#### b. Send additional user information

   Syntax:
    
    HashMap<String, Object> userProperties = new HashMap<>();
    userProperties.put("key1", value1);
    userProperties.put("key2", value2);
    userProperties.put("key3", value3);
    userProperties.put("keyN", valueN);
    UserExperior.setUserProperties(userProperties);
    
   Eg.

    HashMap<String, Object> userProperties = new HashMap<>();
    userProperties.put("USER_NAME", userName);
    userProperties.put("CITY", city);
    userProperties.put("STATE", state);
    userProperties.put("COUNTRY", country);
    userProperties.put("DOB", dob);
    UserExperior.setUserProperties(userProperties);
    
   Note: Please send the Date in "YYYY/MM/DD" format.

### 2. Log Event

UserExperior SDK lets you log user events based on the scenario. An event is the indication of Progress in the user's session. LogEvent() can be used as follows

#### a. Log event with name

   Syntax:
    
    UserExperior.logEvent("Pass-Your-Event-Name-Here");
    
   Eg.
    
    UserExperior.logEvent("Registration Successful");

   Note: Max `eventName` limit is 250 chars only
    
#### b. Log event with name and properties

   Syntax:
    
    HashMap<String, Object> eventProp = new HashMap<>();
    eventProp.put("key1", val1);
    eventProp.put("key2", val2);
    eventProp.put("key3", val3);
    eventProp.put("keyN", valN);
    UserExperior.logEvent("Your-Event-Name", eventProp);
    
   Eg.
    
    HashMap<String, Object> eventProp = new HashMap<>();
    eventProp.put("Mobile_Number", mobileNum);
    eventProp.put("Service_Provider", serviceProvider);
    eventProp.put("Circle", circle);
    eventProp.put("Amount", amount);
    eventProp.put("Date", date);
    UserExperior.logEvent("MOBILE_TOPUP", eventProp);        

   Note: Max `eventName` limit is 250 chars only; Please send the Date in "YYYY/MM/DD" format.

    
### 3. Log Message

UserExperior SDK lets you log user meessage based on the scenario. A message can be any app message shown to the user, any response OR error message OR toast message OR validation messages OR messages shown on dialog boxes, etc. which indicates a response to the user by the app. LogMessage() can be used as follows

#### a. Log message with name

   Syntax:
    
    UserExperior.logMessage("Pass-Your-Message-Here");
    
   Eg.
    
    UserExperior.logMessage("User Name or Password is incorrect");

   Note: Max `messageName` limit is 250 chars only
    
#### b. Log message with name and properties

   Syntax:
    
    HashMap<String, Object> messageProp = new HashMap<>();
    messageProp.put("key1", val1);
    messageProp.put("key2", val2);
    messageProp.put("key3", val3);
    messageProp.put("keyN", valN);
    UserExperior.logEvent("Your-Message", messageProp);
    
   Eg.
    
    HashMap<String, Object> messageProp = new HashMap<>();
    messageProp.put("Consumer_Number", consumerNum);
    messageProp.put("Electricity_Board", electricityBoard);
    messageProp.put("City", city);
    messageProp.put("Amount", amount);
    messageProp.put("Date", date);
    UserExperior.logEvent("Electricity Recharge Successfully Done!", messageProp);
    
  Note: Max `messageName` limit is 250 chars only; Please send the Date in "YYYY/MM/DD" format.
