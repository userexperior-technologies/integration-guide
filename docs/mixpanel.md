# Mixpanel (Android)

## Integration

1. **Switch On the Mixpanel in UserExperior Settings**

  Go to UserExperior Dashboard > Go to your app folder > Go to Settings > Select Integrations > Switch On **Mixpanel**
  
  ![Firebase Crashlytics Switch](_media/firebase-crashlytics-android/firebase-crashlytics-switch.png)

2. **Add UserExperior Listener immediately after startRecording:**

  Add following code in onCreate method of every launcher activity.

  ```
  UserExperior.startRecording(getApplicationContext(), "your-version-key-here");
  
  // UserExperior Listener: Third Party Integration
  UserExperior.setUserExperiorListener(new UserExperiorListener() {
    @Override
    public void onUserExperiorStarted() {
        // Sending UserExperior Session URL to Mixpanel
        String ueSessionUrlMixpanel = UserExperior.getSessionUrl("Mixpanel");
        
        JSONObject props = new JSONObject();
        props.put("UE Session URL", ueSessionUrlMixpanel);
       
        public static final String MIXPANEL_TOKEN = "put-your-mixpanel-project-token-here";

        // Initialize the library with your Mixpanel project token, MIXPANEL_TOKEN, and a reference to your application context.
        MixpanelAPI mixpanel = MixpanelAPI.getInstance(context, MIXPANEL_TOKEN);
        mixpanel.track("UE Session URL", props);
    }
  });
  ```
  
## Replay of Sessions
 
After completing the integration, every Mixpanel session will contain an event called **"UE Session URL"**. You can just copy and paste the URL in your browser's window that will open the session in the UserExperior Dashboard. If the session was recorded you will be able to replay it in the UserExperior Dashboard.
