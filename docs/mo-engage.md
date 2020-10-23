# MoEngage (Android)

## Integration

1. **Switch On the MoEngage in UserExperior Settings**

  Go to UserExperior Dashboard > Go to your app folder > Go to Settings > Select Integrations > Switch On **MoEngage**
  
  ![Firebase Crashlytics Switch](_media/firebase-crashlytics-android/firebase-crashlytics-switch.png)

2. **Add UserExperior Listener immediately after startRecording:**

  Add following code in onCreate method of every launcher activity.

  ```
  UserExperior.startRecording(getApplicationContext(), "your-version-key-here");
  
  // UserExperior Listener: Third Party Integration
  UserExperior.setUserExperiorListener(new UserExperiorListener() {
    @Override
    public void onUserExperiorStarted() {
        // Sending UserExperior Session URL to MoEngage
        String ueSessionUrl = UserExperior.getSessionUrl("MoEngage");
        
        Properties properties = new Properties();
        properties.addAttribute("UE_Session_URL", ueSessionUrl);
        MoEHelper.getInstance(getApplicationContext()).trackEvent("UE_Session_URL", properties);
    }
  });
  ```
  
## Replay of Sessions
 
After completing the integration, every MoEngage session will contain an event called **"UE_Session_URL"**. You can just copy and paste the URL in your browser's window that will open the session in the UserExperior Dashboard. If the session was recorded you will be able to replay it in the UserExperior Dashboard.