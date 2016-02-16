# APPLOZIC WEB PLUGIN     

### Overview      


Integrate messaging into your mobile apps and website without developing or maintaining any infrastructure. Register at https://www.applozic.com         



Want to contribute? Drop us a mail at   ` contact@applozic.com `    


### Getting Started          





****Applozic messaging jQuery plugin****

Integrate messaging plugin into your web application.

A jQuery plugin to integrate messaging into your web page for real time communication between users via Applozic messaging platform and also to see your latest conversations and past chat history.


Add Applozic messaging plugin into your web application :


Step 1: Register at **https://www.applozic.com/** to get the application key.

Step 2: For the standard user interface, add the following Applozic messaging plugin script file before **`</head>`** into your web page:               




```
<script type="text/javascript">
(function(d, m){
  var s, h; s = document.createElement("script");
   s.type = "text/javascript";
   s.async=true;
   s.src="https://apps.applozic.com/sidebox.app";
   h=document.getElementsByTagName('head')[0];
   h.appendChild(s);
   window.applozic=m;
   m.init=function(t){m._globals=t;}})(document, window.applozic || {});
</script>
```
 
 
 
 
 Step 3: Copy and paste below script before **`</body>`** to initialize plugin: 
 
 
 
 
 
``` 
<script type="text/javascript" >
  window.applozic.init({userId: 'PUT_USERID_HERE', appId: 'PUT_APPLICAION_KEY_HERE', desktopNotification: true});
</script>
```    



 Above options description :    



```
 userId: 'USERID from whom you want to initialize plugin'                   // required   
 appId: 'Your Application Key'                       // obtained from Step 1 (required)     
 desktopNotification: true or false                  // optional
 Note : Only for chrome browser enable or disable desktop notifications for incoming messages.
```



Step 4: Some additional options which you can configure while plugin initialization in Step 3 :


```
 1) contactDisplayName: 'PASS_YOUR_FUNCTION_NAME_HERE'  // Type - FUNCTION  (optional)
  Function should return USER_DISPLAY_NAME by taking USERID as input parameter. Example given in Step 5        
 2) contactDisplayImage: 'PASS_YOUR_FUNCTION_NAME_HERE'  //Type - FUNCTION (optional)
  Function should return USER_IMAGE_URL by taking USERID as a input parameter. Example given in Step 6 
 3) onInit : 'PASS_YOUR_FUNCTION_NAME_HERE'  // TYPE - FUNCTION
  Callback function which execute after plugin initialize. You can write your logic inside this function which you want to execute after plugin initialization. Example given in Step 7
```


Sample of **CONTACTS_JSON** given below which is used as a reference in Step 5 and Step 6      


```
var CONTACTS_JSON = {"USERID_1": {"displayName": "Devashish",
"photoLink": "https://www.applozic.com/resources/images/applozic_icon.png"},
"USERID_2": { "displayName": "Adarsh", "photoLink":    
"https://www.applozic.com/resources/images/applozic_icon.png"}, 
"USERID_3": { "displayName": "Shanki", "photoLink":  
"https://www.applozic.com/resources/images/applozic_icon.png"}}; 
 ```



Step 5: Sample code define **contactDisplayName()** function (optional) : 

You  can write javascript function which return USER_DISPLAY_NAME on basis of USERID 

Example:     

```   
 function contactDisplayName(USERID)  {                      
   var contact = CONTACTS_JSON[USERID];               
        if (typeof contact !== 'undefined')             
          {                                      
           return contact.displayName;                  
         } 
 }                     
```


Step 6: Sample code to define **contactDisplayImage()** function (optional) : 

You can write javascript function to return USER_IMAGE_URL on basis of USERID 


Example:     


```
  function contactDisplayImage(USERID)  {                        
    var contact =  CONTACTS_JSON[USERID];                       
    if (typeof contact !== 'undefined')                      
      {                       
        return contact.photoLink;          
      }
  }                            
 ```
 
Step 7: Sample code to define **onInit()** function  (optional) : 

You can write javascript function to execute your logic after plugin initialization


Example:     


  ```
  function onInit(response) {
    if (response === "success") {
      // write your logic here
    }
  };
  
  ```
 
 
 Step 8: If you want to load all contacts directly use below function (optional) :

```
// APPLOZIC_FUNCTION_TO_LOAD_CONTACTS
 $applozic.fn.applozic('loadContacts', 'PUT_CONTACT_LIST_JSON_HERE'); // contacts json format given below
 
 
// SAMPLE CONTACT_LIST_JSON 
var CONTACT_LIST_JSON = 
          {"contacts": [{"userId": "user1", "displayName": "Devashish", 
                          "photoLink": "https://www.applozic.com/resources/images/applozic_icon.png"}, 
                        {"userId": "user2", "displayName": "Adarsh", 
                          "photoLink": "https://www.applozic.com/resources/images/applozic_icon.png"}, 
                        {"userId": "user3", "displayName": "Shanki",
                          "photoLink": "https://www.applozic.com/resources/images/applozic_icon.png"}
                      ]
         };       

```

**NOTE**- Call **loadContacts** function only after plugin initailization.
You don't need to use functions explained in Step 5 and Step 6 if loading all contacts dynamically as explaind in Step 8  



Step 9: Function to load individual tab conversation dynamically (optional) :

```
 $applozic.fn.applozic('loadTab', 'PUT_OTHER_USERID_HERE');  // user Id of other person with whom you want to open conversation 

 ``` 
 
 
 
Step 10: Anchor tag or button to load individual tab conversation directly (optional) :

You can add the following html into your code to directly open a conversation with any user-   

```
<a href="#" class="applozic-launcher" data-mck-id="PUT_OTHER_USERID_HERE" data-mck-name="PUT_OTHER_USER_DISPLAY_NAME_HERE">CHAT BUTTON</a>

**Note** - Data attribute **mck-name** is optional in above tag
 ``` 
 
 
 
Step 11: To add auto suggest users list in search field use below element id (optional) : 

You can bind auto suggest plugin on input search field with id given below     

```
mck-search 
```

  


Step 12: To show **online/offline** status(optional) : 

You can add the following  properties to your html element for real time online/offline status update

**Two Class Attribute** - 
mck-user-ol-status **AND** n-vis



**Data Attribute** - 
data-mck-id='PUT_OTHER_USERID_HERE'


Example: 
```
<div class="mck-user-ol-status n-vis" data-mck-id='PUT_OTHER_USERID_HERE'></div>
```






### Customization     






****Applozic messaging jQuery plugin****

Integrate messaging plugin into your web application.

A small jQuery plugin for integrating messaging into your web page to directly send and receive messages to other users via **Applozic** messaging platform and also to see your latest conversations.

Add Applozic messaging plugin into your web application :


Step 1: Register at **https://www.applozic.com/** to get the application key.


Step 2: For customization an- where you can modify the UI, checkout **https://github.com/AppLozic/Applozic-Web-Plugin/tree/master/message/advanced**

Open **message.html**  file as a reference and add all scripts and html in your web page in same order as given in message.html. 


Step 3: Initialize plugin using script given below also given in message.html (Initialize once page load completely, preferable in document.ready function) :     



```
  $applozic.fn.applozic({userId: 'customer-1', appId: 'applozic-sample-app',        
  ojq: $original,        
  readConversation: readMessage,          
  contactDisplayName: displayName,      
  contactDisplayImage: contactImageSrc,          
  desktopNotification: true          
  }); 
```



Step 4: Change the following parameters in above script :     



 ```
  userId: 'User Unique id',                 // required          
  appId: 'Your application key',             // required \        
  contactDisplayName: 'Callback function to return contact name by userId',      
  // function should receive one parameter i.e userId. Example given in Step:7 (optional)          
  contactDisplayImage: 'Callback function to return image src of contact by userId',        
  // function should receive one parameter i.e userId. Example given in Step:8 (optional)       
  desktopNotification: true or false        
  // for chrome browser enable or disable desktop notifications for incoming messages (optional)              
```


*Note : Examples of callback functions and json format is given in below in step 7,8 and also given in message.html

Step5 : To customize layout of plugin :

You can modify **mck-sidebox-1.0.css** class located at :      



``` 
  https://github.com/AppLozic/Applozic-Web-Plugin/blob/master/message/advanced/css/app/mck-sidebox-1.0.css 
```

Step 6: To add auto suggest users list in search field (optional)

You can bind auto suggest plugin on input search field with id given below:    


```
mck-search 
```

Contacts Json format is given below as a reference used in **displayName()** and **contactImageSrc()** :     


``` 
 var contacts = {"user1": {"userId": "user1", "displayName": "Devashish",
 "photoLink":  "https://www.applozic.com/resources/images/applozic_icon.png"}, 
 "user2": {"userId": "user2", "displayName": "Adarsh", 
 "photoLink": "https://www.applozic.com/resources/images/applozic_icon.png"}, 
 "user3": {"userId": "user3", "displayName": "Shanki", "photoLink": 
 "https://www.applozic.com/resources/images/applozic_icon.png"}}; 
 ```



Step 7: Callback function to get contact display name from userId (optional)

You  can write javascript function which return display name on basis of userId 

Example:         


```
 function displayName(userId)  {                  
   var contact = contacts[userId];  // used contacts variable as given above.      
   if (typeof contact !== 'undefined')    
   {               
   return contact.displayName;       
   } }                          
```

Step 8: Callback function to get contact image url  from userId (optional)

You  can write javascript function to return user image url on basis of userId 

Example:      


```
  function contactImageSrc(userId) {                        
    var contact = contacts[userId];   // used contacts variable as given above.          
    if (typeof contact !== 'undefined')                  
    {               
    return contact.photoLink;               
    } }
```    
    
    



Step 9: Function to load contact list dynamically (optional)

You can call below function to load contact list by passing contacts json as given in variable contacts :      



```
 var contacts = {"contacts": [{"userId": "user1", "displayName": "Devashish",
 "photoLink":  "https://www.applozic.com/resources/images/applozic_icon.png"},
 {"userId": "user2", "displayName": "Adarsh",
 "photoLink": "https://www.applozic.com/resources/images/applozic_icon.png"},
 {"userId": "user3", "displayName": "Shanki", 
 "photoLink": "https://www.applozic.com/resources/images/applozic_icon.png"}]}; 
 
 $applozic.fn.applozic('loadContacts', 'put-contacts-json-here); // contacts json format given above 
 ```


Step 10: Function to load tab dynamically (optional)

You can call below function to directly open any contact tab dynamically :       


```
 $applozic.fn.applozic('loadTab', 'put-userId-here'); 
```              



### Lightweight - Plugin              





**Welcome to the Applozic-Web-Plugin**

# Applozic light weight messaging jQuery plugin.

Integrate messaging plugin into your web application.

Add Applozic messaging plugin into your web application for real time messaging communication 
via  Applozic functions. 

**Step 1**: Register at **https://www.applozic.com/** to get the application key.

**Step 2**: For the standard user interface, add the following Applozic messaging plugin script file before **`</head>`** into your web page:                 





```          
<script type="text/javascript" src="https://www.applozic.com/resources/lib/js/apz-notify.min.js"></script>      
<script type="text/javascript" src="https://www.applozic.com/resources/sidebox/js/app/apz-client-1.0.js"></script>        
```               


**Step 3**: Initialize Plugin - 
Create **APPLOZIC** instance by passing options            



```      
 var applozic = new APPLOZIC({'baseUrl': "https://apps.applozic.com",
 'userId': 'put-userId-here',
 'appId': 'put-applicationKey-here',
'onInit': initResponse // callback function called on initialization
});        
```              



*Note- Create **APPLOZIC** instance only after page load probably inside  **$(document).ready()**. 
function before **`</body>`** 
After  plugin initialization if **onInit** callback function response is  *`success` you can send and receive messages by calling  Applozic functions directly as explained in Step 5 and Step 6 


Step 4:  Subscribe to Applozic events and implement your own logic:
Following are the events with example:                    





```        
applozic.events = {onConnect: function () {
console.log('connected successfully');
}, onConnectFailed: function () {
console.log('connection failed');
}, onMessageDelivered: function (obj) {
console.log('onMessageDelivered: ' + obj);
}, onMessageRead: function (obj) {
console.log('onMessageRead: '  + obj);
}, onMessageReceived: function (obj) {
console.log('onMessageReceived: ' + obj);
}, onMessageSentUpdate: function (obj) {
console.log('onMessageSentUpdate: ' + obj);
}, onUserConnect: function (obj) {
console.log('onUserConnect: ' + obj);
}, onUserDisconnect: function (obj) {
console.log('onUserDisconnect: ' + obj);
},
};              
  ```               
  
  
  
  
  **Events description**:

1) ** onConnect ** : triggered when user subscribed successfully. 
2) **onConnectFailed** :  triggered when user failed to subscribe.
3)  **onMessageDelivered** : triggered when message is delivered. Response contains message key.
 Response object- {'messageKey': 'delivered-message-key'}.
4) **onMessageRead** : triggered when delivered message is read on other end. Response contains message key.
 Response object - {'messageKey': 'delivered-message-key'}.
5) **onMessageReceived** : triggered when new message received. Response contains message
Response object -  {'message': message}  // Message json format given in Step 6.
6) **onMessageSentUpdate** : triggered when message sent successfully to server. Response contains      messageKey.
 Response  object- {'messageKey': 'sent-message-key'}.
7) **onUserConnect **: triggered when some other user comes online. Response contains user Id.
 Response object - {'userId': 'connected-user-Id'}
8) **onUserDisconnect** : triggered when some other user goes offline. Response contains user Id.
Response object - {'userId': 'disconnected-user-id', 'lastSeenAtTime' : 'time in millsec'}



**Step 5** : Send Message -                  




```               
applozic.sendMessage(message, {'callback': sendMessageCallbackFunction});
```        



**message**  include -         




```     
message = { 'to': 'put-userid-here',  // receiver userid
'message': 'message-text' //  message text
};     
```       



**sendMessageCallbackFunction** response -                   



```    
response = { 'status' : 'success', // or 'error'
'response' :  // oblect 
{  'messageKey': 'message-identifier'
'timeStamp': 'message created timestamp'
}                                 
}        
```         



Step 6: **Get Message List** -         




```
applozic.messageList(params, {'callback': messageListCallbackFunction});
```        



 **params**  include-           
 
 
 
 
 
 ```
 params = { 'id': 'put-userid-here'};  // other userid with whom conversations fetch
 ```            
 
 
 
 **messageListCallbackFunction** response -                
 
 
 
 
 
 ```
 response = { 'status' : 'success', // or 'error'
 'messages' :[]  // Array of messages  (message format given below)     
 }
```         



**message** json format-           



```
message = {
key: "message-identifier",
from: "sender userid",         
message: "message-text",
type: 'inbox or outbox',
status: "message status",  // outbox  (sent, delivered or read)
// inbox (read, unread)
timeStamp: 'message created timestamp',
to: 'receiver userid'
 }
```              







 








# ANDROID SDK    


### Overview         



Integrate messaging into your mobile apps and website without developing or maintaining any infrastructure. Register at https://www.applozic.com to get the application id.            





 







### Getting Started       


**** Quick Start for Applozic Messaging ****      



To integrate messaging into your android app, register at [Applozic](https://www.applozic.com/) to get the application key.

** Step 1: Add the following in build.gradle **:      



`compile 'com.applozic.communication.uiwidget:mobicomkitui:3.21' `      


Add the following in gradle android target:      


```
packagingOptions    
 {           
 exclude 'META-INF/DEPENDENCIES'      
 exclude 'META-INF/NOTICE'         
 exclude 'META-INF/LICENSE'      
 exclude 'META-INF/LICENSE.txt'    
 exclude 'META-INF/NOTICE.txt' 
 exclude 'META-INF/ECLIPSE_.SF'
 exclude 'META-INF/ECLIPSE_.RSA'
 }                
```

**Step 2: Addition of Permissions, Services and Receivers in androidmanifest.xml**:

Applozic Application Key:     



```
<meta-data android:name="com.applozic.application.key"
           android:value="YOUR_APPLOZIC_APPLICATION_KEY" /> 

```         
   
Applozic Application URL:        
   
   
   ```
<meta-data android:name="com.applozic.server.url"
           android:value="https://apps.applozic.com" /> 
   ```
    
 Applozic MQTT URL:
 
 ```
 <meta-data android:name="com.applozic.mqtt.server.url"
            android:value="tcp://apps.applozic.com" />
   ```
    
 Applozic Notification package name and launcher icon:        
 
 
```
<meta-data android:name="com.applozic.mobicomkit.notification.icon" 
           android:resource="YOUR_LAUNCHER_ICON" />  
          
```   
```
<meta-data android:name="com.applozic.mobicomkit.notification.smallIcon"
           android:resource="YOUR_LAUNCHER_SMALL_ICON" />
```
```
<meta-data android:name="com.package.name" 
           android:value="${applicationId}" /> 
           
```
   
   
   **Note**: If you are **not using gradle build** you need to replace ${applicationId}  with your Android app package name

Invite Message:


```
<meta-data android:name="share_text"
          android:value="YOUR INVITE MESSAGE" />
  ```

Attachment Folder configuration:         


    
```
<meta-data android:name="main_folder_name"
           android:value="@string/default_media_location_folder" /> 
```
  
  Define below in your string.xml.          
  
  
     
```
<string name="default_media_location_folder"><YOUR_APP_NAME></string> 
```
  
  
  
  
  Register at [Applozic](https://www.applozic.com/) to get the application key.

Permissions:          






```
<uses-permission android:name="<APP_PKG_NAME>.permission.C2D_MESSAGE" />
<permission android:name="<APP_PKG_NAME>.permission.C2D_MESSAGE" android:protectionLevel="signature" />
<uses-permission android:name="com.google.android.c2dm.permission.RECEIVE" />
<uses-permission android:name="android.permission.INTERNET" />
<uses-permission android:name="android.permission.WRITE_EXTERNAL_STORAGE"  />
<uses-permission android:name="android.permission.READ_CONTACTS" />
<uses-permission android:name="android.permission.WRITE_CONTACTS" />
<uses-permission android:name="android.permission.VIBRATE"/>
<uses-permission android:name="android.permission.WAKE_LOCK" />
<uses-permission android:name="android.permission.RECEIVE_BOOT_COMPLETED" />
<uses-permission android:name="android.permission.ACCESS_COARSE_LOCATION" />
<uses-permission android:name="android.permission.ACCESS_FINE_LOCATION" />
<uses-permission android:name="android.permission.ACCESS_NETWORK_STATE" />
<uses-permission android:name="android.permission.READ_EXTERNAL_STORAGE"/>
  ```


Broadcast Registration For PushNotification:        


   
```
<receiver android:name="com.applozic.mobicomkit.uiwidgets.notification.MTNotificationBroadcastReceiver">
   <intent-filter>            
        <action android:name="${applicationId}.send.notification"/>                    
   </intent-filter>           
</receiver>                  
```

**Note**: If you are **not using gradle build** you need to replace ${applicationId}  with your Android app package name



Paste the following in your androidmanifest.xml:       




   
```
 <activity android:name="com.applozic.mobicomkit.uiwidgets.conversation.activity.ConversationActivity"
           android:configChanges="keyboardHidden|orientation|screenSize"
           android:label="@string/app_name"
           android:parentActivityName="<APP_PARENT_ACTIVITY>"
           android:theme="@style/ApplozicTheme"
           android:launchMode="singleTask" >
      <!-- Parent activity meta-data to support API level 7+ -->
<meta-data
           android:name="android.support.PARENT_ACTIVITY"
           android:value="<APP_PARENT_ACTIVITY>" />
 </activity>
                   
<activity android:name="com.applozic.mobicomkit.uiwidgets.people.activity.MobiComKitPeopleActivity"
          android:configChanges="keyboardHidden|orientation|screenSize"
          android:label="@string/activity_contacts_list"
          android:parentActivityName="com.applozic.mobicomkit.uiwidgets.conversation.activity.ConversationActivity"
          android:theme="@style/Applozic.People.Theme"
          android:windowSoftInputMode="adjustResize">
     <!-- Parent activity meta-data to support API level 7+ -->
<meta-data
          android:name="android.support.PARENT_ACTIVITY"
          android:value="com.applozic.mobicomkit.uiwidgets.conversation.activity.ConversationActivity" />
         <intent-filter>
                 <action android:name="android.intent.action.SEARCH" />
         </intent-filter>
<meta-data
          android:name="android.app.searchable"
          android:resource="@xml/searchable_contacts" />
</activity>

<activity android:name="com.applozic.mobicomkit.uiwidgets.conversation.activity.FullScreenImageActivity"
          android:configChanges="keyboardHidden|orientation|screenSize"
          android:label="Image"
 android:parentActivityName="com.applozic.mobicomkit.uiwidgets.conversation.activity.ConversationActivity"
          android:theme="@style/Applozic_FullScreen_Theme">
    <!-- Parent activity meta-data to support API level 7+ -->
<meta-data
          android:name="android.support.PARENT_ACTIVITY"
          android:value="com.applozic.mobicomkit.uiwidgets.conversation.activity.ConversationActivity" />
</activity>
                   
<service android:name="com.applozic.mobicomkit.api.conversation.MessageIntentService"
          android:exported="false" />
              
<service android:name="org.eclipse.paho.android.service.MqttService"/>

<service android:name="com.applozic.mobicomkit.api.conversation.ApplozicIntentService"
         android:exported="false" />
             
<service android:name="com.applozic.mobicomkit.api.conversation.ApplozicMqttIntentService"
         android:exported="false" />

<receiver android:name="com.applozic.mobicomkit.broadcast.NotificationBroadcastReceiver">
         <intent-filter>
                 <action android:name="applozic.LAUNCH_APP" />
         </intent-filter>
<meta-data
          android:name="activity.open.on.notification"
          android:value="com.applozic.mobicomkit.uiwidgets.conversation.activity.ConversationActivity" />
</receiver>

<receiver android:name="com.applozic.mobicomkit.broadcast.TimeChangeBroadcastReceiver">
         <intent-filter>
                 <action android:name="android.intent.action.TIME_SET" />
                 <action android:name="android.intent.action.TIMEZONE_CHANGED" />
         </intent-filter>
</receiver>

<receiver android:name="com.applozic.mobicomkit.broadcast.ConnectivityReceiver"
          android:exported="true" android:enabled="true">
          <intent-filter>
                  <action android:name="android.intent.action.BOOT_COMPLETED" />
                  <action android:name="android.net.conn.CONNECTIVITY_CHANGE" />
          </intent-filter>
</receiver>                  
```






Replace APP_PARENT_ACTIVITY with your app's parent activity.        

**Step 3: Register user account**:     



     
```
UserLoginTask.TaskListener listener = new UserLoginTask.TaskListener() {                  

@Override          
public void onSuccess(RegistrationResponse registrationResponse, Context context)         
{              
}                       

@Override             
public void onFailure(RegistrationResponse registrationResponse, Exception exception)         
{         
}};                      

User user = new User();          
user.setUserId(userId); 
user.setDisplayName(displayName); 
user.setEmail(email); //optional                        
new UserLoginTask(user, listener, this).execute((Void) null);                                      
```

If it is a new user, new user account will get created else existing user will be logged in to the application.

**Step 4: Updating GCM registration id:**

In case, if you don't have the existing GCM related code, then copy the files from https://github.com/AppLozic/Applozic-Android-SDK/tree/master/app/src/main/java/com/applozic/mobicomkit/sample/pushnotification
to your project and add the following lines in the "onSuccess" method mentioned in Step 3.

To Enable Android Push Notification using Google Cloud Messaging (GCM) visit the below link https://blog.applozic.com/enable-push-notification-in-your-android-app-ae591de461e7#.q086bfbgv

After Registering project at https://console.developers.google.com Replace the value of GCM_SENDER_ID in GCMRegistrationUtils.java with your own project gcm sender id.
SenderId is a unique numerical value created when you configure your API project (given as "Project Number" in the Google Developers Console).            




```
 GCMRegistrationUtils gcmRegistrationUtils = new GCMRegistrationUtils(activity);          
 gcmRegistrationUtils.setUpGcmNotification();                      
```

If you already have a GCM code in your app, then copy the following code at the place where you are getting the GCM registration id.       
     
```
PushNotificationTask pushNotificationTask = null         
PushNotificationTask.TaskListener listener = new PushNotificationTask.TaskListener()   
{                  

@Override           
public void onSuccess(RegistrationResponse registrationResponse)             
{            
}            
@Override          
public void onFailure(RegistrationResponse registrationResponse, Exception exception)      
{             
} };                    

pushNotificationTask = new PushNotificationTask(pushnotificationId, listener, mActivity);            
pushNotificationTask.execute((Void) null);                          
```


**Step 5: Handling push notification
**
Add the following in your GcmBroadcastReceiver's onReceive method.     





       
```
if(MobiComPushReceiver.isMobiComPushNotification(intent))       
{            
MobiComPushReceiver.processMessageAsync(context, intent);               
return;          
}                     
```


**Step 6: For starting the messaging activity**:        

      
```
Intent intent = new Intent(this, ConversationActivity.class);            
startActivity(intent);                               
``` 
 
 
 For starting individual conversation thread, set "userId" in intent:        
 
           
```
Intent intent = new Intent(this, ConversationActivity.class);            
intent.putExtra(ConversationUIService.USER_ID, "devashish@applozic.com");             
intent.putExtra(ConversationUIService.DISPLAY_NAME, "Devashish Mamgain"); //put it for displaying the title.             
startActivity(intent);                              
```


For easy insertion of Admin/Support Contact information, please changes following values in string.xml. You can take sample app method ( MainActivity.buildSupportContactData() ) as reference for contact information insertion.          




          
```
<string name="support_contact_display_name">AppLozic Support</string>               
<string name="support_contact_userId">applozic</string>             
<string name="support_contact_emailId">devashish@applozic.com</string>              
<string name="support_contact_number">918042028425</string>              
<string name="support_contact_image_url">R.drawable.ic_launcher</string>                                  
```

support_contact_image_url also supports url eg:
 https://www.applozic.com/resources/sidebox/images/applozic.png

**Step 7: On logout, call the following**:       




 new UserClientService(this).logout();      
 
 
 
 Note: If you are running ProGuard, please add following lines:        
 
 
 
 
 
```
 #keep json classes                
 -keepclassmembernames class * extends com.applozic.mobicomkit.api.JsonMarker         
 {            
 !static !transient <fields>;                  
 }              
 #GSON Config          
-keepattributes Signature          
-keep class sun.misc.Unsafe { *; }           
-keep class com.google.gson.examples.android.model.** { *; }            
-keep class org.eclipse.paho.client.mqttv3.logging.JSR47Logger { *; }                                    
 ``` 
   
   
   
   
Trying out the demo app:

Open project in Android Studio to run the sample app in your device. Send messages between multiple devices. 


Display name for users:
You can either choose to handle display name from your app or have Applozic handle it.
From your app's first activity, set the following to disable display name feature:
ApplozicClient.getInstance(this).setHandleDisplayName(false);
By default, the display name feature is enabled.

UI Customization:

Clone the repository : [https://github.com/AppLozic/Applozic-Android-SDK](https://github.com/AppLozic/Applozic-Android-SDK)

Import [MobiComKitUI Library](https://github.com/AppLozic/Applozic-Android-SDK/tree/master/mobicomkitui)  into your android project and add the following in the build.gradle file:

compile project(':mobicomkitui')


MobiComKitUI contains the ui related source code, icons, layouts and other resources which you can customize based on your design needs.

For your custom contact list, replace MobiComKitPeopleActivity with your contact list activity.

Sample app with integration is available under [app](https://github.com/AppLozic/Applozic-Android-SDK/tree/master/app)










### Messages             

Classes ending with *ClientService.java interacts with the server.


**1. Account registration**:      
   
Class: com.applozic.mobicomkit.api.account.register.RegisterUserClientService      



```
new RegisterUserClientService(activity).createAccount
(USER_EMAIL, USER_ID, USER_PHONE_NUMBER, GCM_REGISTRATION_ID);         
 ``` 

**2. Send message**:    

Class: com.applozic.mobicomkit.api.conversation.MobiComConversationService         



```
 public void sendMessage(Message message)        
 {             
   ...        
 }                
```

Example: new MobiComConversationService(activity).sendMessage(new     
Message("contact@applozic.com", "hello test"));         



**3. Message list**:      

Class: com.applozic.mobicomkit.api.conversation.MobiComConversationService

  
i) Get single latest message from each conversation        




```
 public synchronized List<Message> getLatestMessagesGroupByPeople()        
 {            
  ...         
 }                              
```


ii) Get messages of logged in user with another user by passing userId, startTime and      
 endTime. startTime and endTime are considered in time in milliseconds from 1970.       




```
 public List<Message> getMessages(String userId, Long startTime, Long endTime)        
 {            
  ...           
 }                           
```



###  Contacts           



***Building your own contacts***         



You can build your own contact in two easy steps by using AppContactService.java api. Sample method **buildContactData()** for adding contacts is present in sample app MainActivity.java.

**Step 1: Build your contact object:**         



```
    Contact contact = new Contact();            
    contact.setUserId(<userId>);           
    (Unique ID to identify contact )                 
    contact.setFullName(<full name of contact>);                 
    contact.setEmailId(<EmailId>);               
    contact.setImageURL(<image http URL OR android resource drawable  >);               
    (in case of drawable use R.drawable.<resource_name>)                         
```

Example :        


```
    Contact contact = new Contact();                 
    contact.setUserId("adarshk");           
    contact.setFullName("Adarsh");               
    contact.setImageURL("R.drawable.applozic_ic_contact_picture_holo_light");           
    contact.setEmailId("applozic.connect@gmail.com");                
```

**Step 2: add contacts :**

After creating contact object in step1, add your contact using AppContactService.java add() method.
 
Example :        



```
    Context context = getApplicationContext();           
    AppContactService appContactService = new AppContactService(context);            
    appContactService.add(contact);                           
```



**AppContactService.Java at a glance**



AppContactService.java provides methods you need to add, delete and update contacts.

**add(Contact contact)** :  Add single contact.

**addAll(List<Contact> contactList)** : Add multiple contacts.

**deleteContact(Contact contact)** : Delete contact.

**deleteContactById(String contactId)** : Delete contact by Id.

**getContactById(String contactId )** : Read contact by Id.

**updateContact(Contact contact)** : Update contact.

**upsert(Contact contact)** : update or insert contact.      



### Group 


***1) Group create Method***  

Create the Group with Group Name and Group Members. The below code illustrator creation of group 
  ```
  String groupName = "Applozic Group"; // Name of group.
  List<String> groupMemberList = new ArrayList<String>(); // List Of unique group member Names.
  groupMemberList.add("member1");
  groupMemberList.add("member2");
  groupMemberList.add("member3");
  groupMemberList.add("member4");
  ```
  After adding group Memebers to List then pass the Group Name and Group Member List to constructor below
  
  Class to import : com.applozic.mobicomkit.api.people.ChannelCreate
  ```
  ChannelCreate channelCreate = new ChannelCreate(groupName,groupMemberList); // The Constructor accepts the two parameter String Group Name and List of Group Members.
  ```
  Class to import : com.applozic.mobicomkit.channel.service.ChannelService
 ```
 ChannelService.getInstance(context).createChannel(channelCreate); // Instantiating the  group create and it accetps the ChannelCreate object.
 ```



### UI Customization


***1.Changing the Chat Bubble Color***

Sent Message bubble color
 ```
ApplozicSetting.getInstance(context).setSentMessageBackgroundColor(int color); // it accepts the R.color.name
 ```
Received Message bubble color

 ```
ApplozicSetting.getInstance(context).setReceivedMessageBackgroundColor(int color); // it accepts the R.color.name
 ```

***2.Changing the Send Bubble Color***

 ```
ApplozicSetting.getInstance(context).setSendButtonBackgroundColor(int color); // it accepts the R.color.name

 ```

***3.To show the Online in Quick Chat Screen***

 ```
ApplozicSetting.getInstance(context).showOnlineStatusInMasterList();

 ```











###  Migrating from 3.019



***Migrating to latest version of Applozic android Sdk***



**Replace the following in build.gradle :**


`compile 'com.applozic.communication.uiwidget:mobicomkitui:3.21' `

**Add meta data in  androidmanifest.xml** 

```
 <meta-data android:name="com.applozic.mqtt.server.url"
            android:value="tcp://apps.applozic.com" />
```

**Replace the old Theme style  of MobiComKitPeopleActivity.java in androidmanifest.xml with @style/Applozic.People.Theme Like below**

```
<activity android:name="com.applozic.mobicomkit.uiwidgets.people.activity.MobiComKitPeopleActivity"
          android:configChanges="keyboardHidden|orientation|screenSize"
          android:label="@string/activity_contacts_list"
          android:parentActivityName="com.applozic.mobicomkit.uiwidgets.conversation.activity.ConversationActivity"
          android:theme="@style/Applozic.People.Theme"
          android:windowSoftInputMode="adjustResize">
     <!-- Parent activity meta-data to support API level 7+ -->
<meta-data
          android:name="android.support.PARENT_ACTIVITY"
          android:value="com.applozic.mobicomkit.uiwidgets.conversation.activity.ConversationActivity" />
         <intent-filter>
                 <action android:name="android.intent.action.SEARCH" />
         </intent-filter>
<meta-data
          android:name="android.app.searchable"
          android:resource="@xml/searchable_contacts" />
</activity>
```




# PLATFORM API     

### Overview        


Integrate native app message communication to your product without developing and maintaining any infrastructure.
Are you looking for platform-native Sdks to integrate into your app. All you need to do is include the Applozic SDK as a library in your project and a couple of lines of code. We will take care of rest things from server hosting, database, maintenance to analytics.     


### Rest API         




****REGISTRATION API****        




**Registration URL**: https://apps.applozic.com/rest/ws/register/client

**Method Type**: POST

**Content-Type**: application/json, application/xml

**Parameters**: Json will be passed as a parameter with following properties :-         




| Parameter  | Required | Default | Description |
| ------------- | ------------- | ------------- | ------------- |       
| userId  | Yes  |   | User name  |
| emailId  | No  | null  | User email address  |
| password  | No  | null  | User account password  |
| displayName  | No  |   | Name you want to display to other user  |  
| applicationId  | Yes  |   | Your Applozic Application key configured in dashboard  |
| deviceType  | Yes  |   | 1 or 4   | 




**Note**:-  deviceType value should be **1** for Android device and **4** for Ios device.




** json **                         
```
{"userId":"abc","deviceType":"4","applicationId":"applozic-sample-app"
}
```


**Response**:  success Response Json to the request with following properties :-         



| Response  | Description |
| ------------- | ------------- |
| message | One of the following is returned: REGISTERED,REGISTERED.WITHOUTREGISTRATIONID, UPDATED |
| userKey | User key  |
| deviceKey  | User device key |
| lastSyncTime  | Time in miliseconds when user device last synced with server  |  
| currentTimeStamp  | Time in miliseconds when response is return from server | 




** json **                         
```
{    "message": "REGISTERED.WITHOUTREGISTRATIONID","userKey": "21fea543-2ade-494f-b905-6bab308d1b4f",
"deviceKey": "09c5d869-6d38-4d6b-9ebf-9de16cdab176","lastSyncTime": 1454328502029, "currentTimeStamp": 1454328502023}
```



***Note** :- **deviceKey** need to be stored and  sent in request header in each API call.




If registration process failed then json response with description :-




** json **                         
```
{  "message": "INCOMPLETE_EMAILID","currentTimeStamp": 1454328359265 }
```



** json **                         
```
{  "message": "INVALID_APPLICATIONID","currentTimeStamp": 1454328359295 }
```




****Authentication Headers From Device****    




Authentication is done using BASIC authentication.

Use **deviceKey** from above  registration response to create Authorization Code and send **deviceKey** also  in request header.
 
**Authorization Code** : Basic Base64Encode of userId:deviceKey




**Example**- 
If the userId is **abc** and deviceKey is **09c5d869-6d38-4d6b-9ebf-9de16cdab176**, then the authorization code will be:

Authorization Code: Basic YWJjOjA5YzVkODY5LTZkMzgtNGQ2Yi05ZWJmLTlkZTE2Y2RhYjE3Ng==




**All request  from Device should contain these 4 headers** -           


| Authorization: Authorization Code  |
| ------------- |
| UserId-Enabled:true |
| Application-Key:  Your Application Key  |  
| Device-Key:  received in registration response  | 




****WEB-PLUGIN INITIALIZE URL****   




**Web-Plugin initialize Url**: https://apps.applozic.com/tab/initialize.page

**Method Type**: GET

**Parameters**:       




| Parameter  | Required | Default  | Description |
| ------------- | ------------- | ------------- | ------------- |
| applicationId  | Yes  |   | Your Application Key  |
| userId  | Yes  |   | User unique Id  |   
| userName  | No  |   |Name you want to display to other user |   




**Response**:  success Response Json to request with following properties :-         

 


** json **
``` 
{"token":"agpzfmFwcGxvemljchMLEgZTdVVzZXIYgICAgOTcwAsM","email":"","userId":"Pink","clientId":"paho2555012084064505","countryCode":"IN","deviceKey":"bf845261-5a1b-4782-bbd2-f23fdf249df6","timeZoneOffset":"19800000","websocketUrl":"https://apps.applozic.com","fileBaseUrl":"https://applozic.appspot.com"} 
```




****Authentication Headers From Web****    




Authentication is done using BASIC authentication.

Use **deviceKey** from above response to create Authorization Code: 
 
**Authorization Code** : Basic Base64Encode of userId:deviceKey




**Example**- 

If the userId is **Pink** and deviceKey is **bf845261-5a1b-4782-bbd2-f23fdf249df6**, then the authorization code will be:

Authorization Code: Basic UGluazpiZjg0NTI2MS01YTFiLTQ3ODItYmJkMi1mMjNmZGYyNDlkZjY=




**All request  from Web should contain these 3 headers** -           


| Authorization: Authorization Code  |
| ------------- |
| UserId-Enabled:true |
| Application-Key:  Your Application Key  |  




**Note**:- Device-Key in request header only sent from device.




****Send Message****   




**SEND MESSAGE URL**: https://apps.applozic.com/rest/ws/message/send

**Method Type**: POST

**Content-Type**: application/json, application/xml

**Parameters**:json will be passed as a parameter with following properties :-               




| Parameter  | Required | Default  | Description |
| ------------- | ------------- | ------------- | ------------- |
| to  | Yes  |   | UserId to which you want to send message |
| message  | Yes  |   | Text Message |




** json **                         
```
{ "to":"XYZ", "message":"Hi XYZ " }
```



**Response**:-       



| Response  | Description |
| ------------- | ------------- |
| message key  | Request is successfully processed  |
| createdAt  | time in milliseconds |




** json **                         
```
{ "messageKey": "5-22bf4626-9019-4a4a-8565-6c0e40ecda96-1454398305364",
  "createdAt": 1454398305000}
```




****Message List****        




**MESSAGE LIST URL**: https://apps.applozic.com/rest/ws/message/list

**Method Type**: GET

**Parameters**:        



| Parameter  | Required | Default  | Description |
| ------------- | ------------- | ------------- | ------------- |
| startIndex  | Yes  | 0  | Starting Index to fetch messages from list.  | 
| pageSize  | Yes  | 50  | Number of messages per page you want to fetch.  |
| startTime  | No  |   | Start Time from when you want to fetch message list. It is number of milliseconds since January 1, 1970, 00:00:00 GMT.  |
| endTime  | No  |   | End Time upto when you want to fetch message list. It is number of milliseconds since January 1, 1970, 00:00:00 GMT.  | 
 
 



**Note**: For fetching the next page of your message list startIndex value should be equal to the sum of pageSize value of all the previous calls.


**Response**:         




 ```  
{"message":[{"key":"5-35c2957b-8de0-482b-bea9-7c5c2e1dd2f4-1452080064726","userKey":"35c2957b-8de0-482b-bea9-7c5c2e1dd2f4","to":"bingo","contactIds":"bingo","message":"how are you","sent":true,"delivered":false,"read":false,"createdAtTime":1452080064000,"type":5,"source":1,"status":3,"pairedMessageKey":"4-35c2957b-8de0-482b-bea9-7c5c2e1dd2f4-1452080064726","contentType":0}]}      
 ```           
 
 
 
 **In Case of Error**:-  
 
 
 
 
| Response  | Description | 
| ------------- | ------------- | 
| error  | In case of any exception or error contact devashish@applozic.com  |
       



****Delete Message****     




**DELETE MESSAGE  URL**: https://apps.applozic.com/rest/ws/message/delete

**Method Type**: GET 

**Parameters**:         



| Parameter  | Response | Default  | Description |
| ------------- | ------------- | ------------- | ------------- |
| key  | Yes  |   | Message unique key  |




**Response**:        



 | Parameter  | Description | 
| ------------- | ------------- | 
| success  | Request is successfully processed  |
| error  |This will come if any exception occurs on server. In case of any exception contact devashish@applozic.com  |




****Delete Conversation Thread ****           



**DELETE CONVERSATION THREAD URL** : https://apps.applozic.com/rest/ws/message/delete/conversation

**Method Type**: GET 

**Parameters**:          



| Parameter  | Response | Default  | Description |
| ------------- | ------------- | ------------- | ------------- |
| userId  | Yes  |   | User for which you want to delete thread  |         





**Response**:           




| Parameter  | Description | 
| ------------- | ------------- | 
| success  | Request is successfully processedl  |
| error  |This will come if any exception occurs on server or all the parameters are null. In case of any exception contact devashish@applozic.com  |
      




****Group Creation **** 



**GROUP CREATION URL**: https://apps.applozic.com/rest/ws/group/create 

**Method Type**: POST 

**ContentType**: application/json, application/xml



**Parameters**: Json will be passed as a parameter with following properties :-    



| Parameter  | Required | Default  | Description |
| ------------- | ------------- | ------------- | ------------- |
| groupName | Yes  |   | Name of the group |
| groupMemberList | Yes  |   |List of names of the  group members |
| type | No  | public  | Type of the group |



**Parameter Example**:   (Suppose "TestUser" is the user calling group creation API)



** json **  

```
{"groupName":"BOYZZ","groupMemberList":["A","B","C"]}
```


 
**Response**: Response Json  with success status :-  



** json **                         
```
{"status":"success","generatedAt":1452342819495,"response":{"id":176,"name":"BOYZZ","adminName":"TestUser","membersName":["A","TestUser","B","C"],"unreadCount":0,"type":2}}
```




**Note**: "type":2 represents the public Group.


****Groups List Of User**** 



**LIST URL**:  https://apps.applozic.com/rest/ws/group/list 

**Method Type**: GET



**Parameters**:        



| Parameter  | Required | Default  | Description |
| ------------- | ------------- | ------------- | ------------- |
| updatedAt | No  |   | lastSyncTime to the server  |
 


**Response**:   Response Json with success status :-         



 ```  
{"status":"success","generatedAt":1452345715245,"response":[{"id":177,"name":"BOYZZ","adminName":"TestUser","membersName":["AB","B","C","TestUser"],"unreadCount":0,"type":2}]}   

 ```



**Note**: Next time when sync to  the server you have option to get information about only modified group and newly added group of that user,for that you have to pass "updatedAt" parameter in Api call. Whenever last time you interacted our server,in response Json you get "generatedAt" parameter ,that value will be used for "updatedAt"("generatedAt":1452345715245) to get the list of only newly added  and modified groups  of the user.





****Delete group**** 



**DELETE GROUP URL**:  https://apps.applozic.com/rest/ws/group/delete 

**Method Type**: GET



**Parameters**: 



| Parameter  | Required | Default  | Description |
| ------------- | ------------- | ------------- | ------------- |
| groupId   | Yes  |   | group unique id  |



**Response**:  Response Json  with success status :-  



 ```  
{"status":"success","generatedAt":1452347180639,"response":"success"}   

 ```



**Note**:Only Admin User can delete the group otherwise you can get following error.



**Response**:  Json with error status :-  



 ```  
{"status":"error","errorResponse":[{"errorCode":"AL-UN-01","description":"unauthorized user","displayMessage":"Unable to process"}],"generatedAt":1452348983616} 

 ```




****Remove  Group member**** 



**REMOVE GROUP MEMBER URL**:  https://apps.applozic.com/rest/ws/group/remove/member 

**Method Type**: GET



**Parameters**: 



| Parameter  | Required | Default  | Description |
| ------------- | ------------- | ------------- | ------------- |
| groupId   | Yes  |   | group unique id  |
| userId   | Yes  |   | name of the user want to remove from group  |



**Response**:  Response Json  with success status :-  



 ```  
{"status":"success","generatedAt":1452347180639,"response":"success"}   

 ```



**Note**:Only Admin User can remove the grop member otherwise you can get following error.



**Response**: Json with error status :-  



 ```  
{"status":"error","errorResponse":[{"errorCode":"AL-UN-01","description":"unauthorized user","displayMessage":"Unable to process"}],"generatedAt":1452348983616} 

 ```


****Leave Group**** 



**LEAVE GROUP URL**:  https://apps.applozic.com/rest/ws/group/left 

**Method Type**: GET



**Parameters**: 



| Parameter  | Required | Default  | Description |
| ------------- | ------------- | ------------- | ------------- |
| groupId   | Yes  |   | group unique id  |




**Response**: Response Json with success status :-  



 ```  
{"status":"success","generatedAt":1452347180639,"response":"success"}   

 ```



****Add Group Member****



**ADD GROUP MEMBER URL**:  https://apps.applozic.com/rest/ws/group/add/member 

**Method Type**: GET



**Parameters**: 



| Parameter  | Required | Default  | Description |
| ------------- | ------------- | ------------- | ------------- |
| groupId   | Yes  |   | group unique id  |
| userId   | Yes  |   | name of the user want to add to the group  |



**Response**:  Response Json with success status :-  



 ```  
{"status":"success","generatedAt":1452347180639,"response":"success"}   

 ```



****Change Group Name****



**CHANGE GROUP NAME URL**:  https://apps.applozic.com/rest/ws/group/change/name 

**Method Type**: POST

**ContentType**: application/json, application/xml



**Parameters**:  Json will be passed as a parameter with following properties :-    



| Parameter  | Required | Default  | Description |
| ------------- | ------------- | ------------- | ------------- |
| groupId| Yes  |   | group unique id |
| newName | Yes  |   |new name of group |




**Response**: Response Json with success status :-  



 ```  
{"status":"success","generatedAt":1452347180639,"response":"success"}   

 ```
 
 
 
 
 
 
 
 
 # IOS SDK           


### Overview        




Integrate messaging into your mobile apps and website without developing or maintaining any infrastructure. Register at https://www.applozic.com to get the application id.


  








### Getting Started                 




**Create your Application**

a )  [**Sign-up**](https://www.applozic.com/signup.html)  with applozic to get your applicationId.

b ) Once you signed up create your Application with required details on admin dashboard. Upload your push-notification certificate to our portal to enable real time notification.         




![dashboard-blank-content](https://raw.githubusercontent.com/AppLozic/Applozic-Chat-SDK-Documentation/master/Resized-dashboard-blank-page.png)         



c) Once you create your application you can see your application-Id listed on admin dashboard. Please use same applicationId explained in further steps.          




![dashboard-blank-content](https://raw.githubusercontent.com/AppLozic/Applozic-Chat-SDK-Documentation/master/Resized-dashboard-content-page.png)         





**Installing the iOS SDK** 

**ADD APPLOZIC FRAMEWORK **
Clone or download the SDK (https://github.com/AppLozic/Applozic-iOS-SDK)
Get the latest framework "Applozic.framework" from Applozic github repo [**sample project**](https://github.com/AppLozic/Applozic-iOS-SDK/tree/master/sampleapp)

**Add framework to your project:**

i ) Paste Applozic framework to root folder of your project. 
ii ) Go to Build Phase. Expand  Embedded frameworks and add applozic framework.         




![dashboard-blank-content](https://raw.githubusercontent.com/AppLozic/Applozic-Chat-SDK-Documentation/master/Resized-adding-applozic-framework.png)        


**Quickly Launch your chat**


You can test your chat quickly by adding below .h and .m file to your project.

[**DemoChatManager.h**](https://raw.githubusercontent.com/AppLozic/Applozic-iOS-SDK/master/sampleapp/applozicdemo/DemoChatManager.h)        

[**DemoChatManager.m**](https://raw.githubusercontent.com/AppLozic/Applozic-iOS-SDK/master/sampleapp/applozicdemo/DemoChatManager.m)  

Change applicationID in DemoChatManager and you are ready to launch your chat from your controller :)

Launch your chat

```
//Replace with your applicationId in DemoChatManager.h

#define APPLICATION_ID @"applozic-sample-app" 


//Launch your Chat from your controller.
 DemoChatManager * demoChatManager = [[DemoChatManager alloc]init];
    [demoChatManager launchChat:<yourcontrollerReference> ];

```

Detail about user creation and registraion:


**USER REGISTRATION :**

**Create a user : ** 
After your app login validation, copy the following code to create applozic user and register your user with applozic server.           


** Objective-C **   
```
 ALUser *user = [[ALUser alloc] init];           
 [user setApplicationId:@"applozic-sample-app"]; // REPLACE SAMPLE ID with your application-Id                
 [user setUserId:[self.userIdField text]]; //replace [self.userIdField text] with user's unique id here                    
 [user setEmailId:[self.emailField text]]; //optional                       
```
   
   
   **Register user with Applozic server :**       
   
   
** Objective-C **
```
  ALRegisterUserClientService *registerUserClientService = [[ALRegisterUserClientService alloc] init];           
  [registerUserClientService initWithCompletion:user withCompletion:^(ALRegistrationResponse *rResponse, 
  NSError *error)       
  {             
  if (error)        
  {             
     NSLog(@"%@",error);            
     UIAlertView *alertView = [[UIAlertView alloc] initWithTitle:@"Response"                
     message:rResponse.message delegate: nil cancelButtonTitle:@"Ok"          
     otherButtonTitles: nil, nil];            
     [alertView show];             
      return ;                  
  }                      
  
   if (rResponse && [rResponse.message containsString: @"REGISTERED"])               
   {                 
     ALMessageClientService *messageClientService = [[ALMessageClientService alloc] init];             
     [messageClientService addWelcomeMessage];             
     }        
     NSLog(@"Registration response from server:%@", rResponse);               
   }];                                       
```



**PUSH NOTIFICATION REGISTRATION AND HANDLING **

**a ) Send device token to applozic server:**

In your AppDelegate’s **didRegisterForRemoteNotificationsWithDeviceToken **method  send device registration to applozic server after you get deviceToken from APNS. Sample code is as below:             




** Objective-C **      
```
 - (void)application:(UIApplication*)application didRegisterForRemoteNotificationsWithDeviceToken:(NSData*)
   deviceToken       
   {                
  
    const unsigned *tokenBytes = [deviceToken bytes];            
    NSString *hexToken = [NSString stringWithFormat:@"%08x%08x%08x%08x%08x%08x%08x%08x",                 
    ntohl(tokenBytes[0]), ntohl(tokenBytes[1]), ntohl(tokenBytes[2]),             
    ntohl(tokenBytes[3]), ntohl(tokenBytes[4]), ntohl(tokenBytes[5]),             
    ntohl(tokenBytes[6]), ntohl(tokenBytes[7])];              
    
    NSString *apnDeviceToken = hexToken;            
    NSLog(@"apnDeviceToken: %@", hexToken);                  
 
   //TO AVOID Multiple call to server check if previous apns token is same as recent one, 
   if different call app lozic server.           

    if (![[ALUserDefaultsHandler getApnDeviceToken] isEqualToString:apnDeviceToken])              
    {                         
       ALRegisterUserClientService *registerUserClientService = [[ALRegisterUserClientService alloc] init];          
       [registerUserClientService updateApnDeviceTokenWithCompletion
       :apnDeviceToken withCompletion:^(ALRegistrationResponse
       *rResponse, NSError *error)       
     {              
       if (error)         
          {          
             NSLog(@"%@",error);             
            return ;           
          }              
    NSLog(@"Registration response from server:%@", rResponse);                         
    }]; } }                                 

```


**b) Receiving push notification:**

Once your app receive notification, pass it to applozic handler for applozic notification processing.             


** Objective-C **      
  ```
  - (void)application:(UIApplication*)application didReceiveRemoteNotification:(NSDictionary*)dictionary         
  {            
   NSLog(@"Received notification: %@", dictionary);           
   
   ALPushNotificationService *pushNotificationService = [[ALPushNotificationService alloc] init];        
   BOOL applozicProcessed = [pushNotificationService processPushNotification:dictionary updateUI:
   [[UIApplication sharedApplication]     applicationState] == UIApplicationStateActive];             
  
    //IF not a appplozic notification, process it            
  
    if (!applozicProcessed)            
      {                
         //Note: notification for app          
    } }                                                           
```


**c) Handling app launch on notification click :**          


** Objective-C **    
```
 - (BOOL)application:(UIApplication *)application didFinishLaunchingWithOptions:(NSDictionary *)launchOptions    
  {                     
  // Override point for customization after application launch.                              
  NSLog(@"launchOptions: %@", launchOptions);                  
  if (launchOptions != nil)               
  {             
  NSDictionary *dictionary = [launchOptions objectForKey:UIApplicationLaunchOptionsRemoteNotificationKey];         
  if (dictionary != nil)             
    {          
      NSLog(@"Launched from push notification: %@", dictionary);        
      ALPushNotificationService *pushNotificationService = [[ALPushNotificationService alloc] init];            
      BOOL applozicProcessed = [pushNotificationService processPushNotification:dictionary updateUI:NO];               
  if (!applozicProcessed)                 
     {            
       //Note: notification for app              
     } } }                                   
      return YES;                 
  }                             

```


**Launching applozic message screen** 

Below code will explain how to launch applozic message view. you can put this according to your need (like on click of any button, add any button at the navigation bar or tab ).            


** Objective - C **     
```
   UIStoryboard* storyboard = [UIStoryboard storyboardWithName:@"Applozic"              
   bundle:[NSBundle bundleForClass:ALMessagesViewController.class]];              
   UIViewController *theTabBar = [storyboard instantiateViewControllerWithIdentifier:@"messageTabBar"];          
   [self presentViewController:theTabBar animated:YES completion:nil];                     
```




**Launching specific user's conversation:
**
To launch conversation for a particular user (most common use case is to launch customer support conversation directly), use below code:         




** Objective - C **        
```
UIStoryboard* storyboard = [UIStoryboard storyboardWithName:@"Applozic"                 
bundle:[NSBundle bundleForClass:ALChatViewController.class]];             
ALChatViewController *chatView =(ALChatViewController*) [storyboard 
instantiateViewControllerWithIdentifier:@"ALChatViewController"];                
chatView.contactIds =@"<USER_ID>";//SET specific USER'S ID                  
UINavigationController *conversationViewNavController = 
[[UINavigationController alloc] initWithRootViewController:chatView]; 
[self presentViewController:conversationViewNavController animated:YES completion:nil];                               
    
```    
    
    
 **Note : make sure you have already registered your login user(User Registration) and completed  push notification registration before launching Applozic message screen.**          
    
    
    
****Logout****           
    
    
    
    
Paste the following code on logout.             
    
    
** Objective - C **           
  ```
  ALRegisterUserClientService *registerUserClientService = [[ALRegisterUserClientService alloc] init];              
  [registerUserClientService logout];                       
  ```
  
  
  
### Building Contacts             




Applozic framework provides convenient APIs for building your own contact. Developers can build and store contacts in three different ways. 

 **Build your contact:** 

** a ) Simple method to create your contact is to create contact object.
**                 




** Objective - C **        
```
ALContact *contact1 = [[ALContact alloc] init];              
contact1.userId = @"adarshk"; // unique Id for user               
contact1.fullName = @"Rathan"; // Fullname of the contact.               

//Display name for contact. This name would be displayed to the user in chat and contact list.                  
contact1.displayName = @"Rathan";               
contact1.email = @"123@abc.com"; //Email Id for the contact.              
//Contact image url. Contact image would be downloaded automatically from URL.                  
ontact1.contactImageUrl =@" https://www.applozic.com/resources/images/applozic_logo.gif";        
contact1.localImageResourceName = @"4.jpg"; // If this field is mentioned,
Contact image will be taken from local storges.   
```


**b) Building contact from dictionary:
**
you can directly build contact from dictionary,all you have to do is just pass a dictionary while initialising obJect.          




** Objective -C **  
```
  //Contact ------- Example with dictonary 
  NSMutableDictionary *demodictionary = [[NSMutableDictionary alloc] init]; 
  [demodictionary setValue:@"aman999" forKey:@"userId"]; 
  [demodictionary setValue:@"aman sharma" forKey:@"fullName"]; 
  [demodictionary setValue:@"aman" forKey:@"displayName"];  
  [demodictionary setValue:@"aman@applozic.com" forKey:@"email"]; 
  [demodictionary setValue:@"http://images.landofnod.com/is/image/LandOfNod/ 
  Letter_Giant_Enough_A_231533_LL/$web_zoom$&wid=
  550&hei=550&/1308310656/not-giant-enough-letter-a.jpg" forKey:@"contactImageUrl"]; 
  [demodictionary setValue:nil forKey:@"localImageResourceName"];              
  ALContact *contact5 = [[ALContact alloc] initWithDict:demodictionary];                   
```




**b) Building contact from JSON:
**           



** Objective -C **       
```
//Contact -------- Example with json                   
NSString *jsonString =@"{\"userId\": \"applozic\",\"fullName\": \"Applozic\",
\"contactNumber\": \"9535008745\",\"displayName\":  \"Applozic Support\",
\"contactImageUrl\": \"https://applozic.com/resources/images/aboutus/rathan.jpg\",\"email\":       
\"devashish@applozic.com\",\"localImageResourceName\":null}";                    
ALContact *contact4 = [[ALContact alloc] initWithJSONString:jsonString];                        
 ```
 
 
 
 **Save Your Contact:** 

Once contacts has been created, you need to save it.  APIs are provided by Applozic to save contacts. 

**saving single contact:
**              


** Objective - C **    
 ```
  ALContactDBService * alContactDBService = [[ALContactDBService alloc]init];                  
  [ alContactDBService addContact:contact];                                 
```


You can build your contact service using applozic contact apis. Below is the sample ContactService given:               






** Objective - C **            
```
 //                    
 //  ALContactService.m                
 //  ChatApp              
 //                
 //  Created by Adarsh on 23/10/15.                   
 //  Copyright © 2015 AppLogic. All rights reserved.                  
 //

  #import "ALContactService.h"                 
  #import "ALContactDBService.h"              
  #import "ALDBHandler.h"                  

  @implementation ALContactService                 

  ALContactDBService * alContactDBService;                      

  -(instancetype)  init{              
     self= [super init];              
     alContactDBService = [[ALContactDBService alloc]init];              
     return self;                   
   }                            

  #pragma mark Deleting APIS               


  //For purgeing single contacts              

  -(BOOL)purgeContact:(ALContact *)contact{               
   return [ alContactDBService purgeContact:contact];             
   }                


  //For purgeing multiple contacts                
  -(BOOL)purgeListOfContacts:(NSArray *)contacts{                
    
  return [ alContactDBService purgeListOfContacts:contacts];               
   }               


  //For delting all contacts at once              

  -(BOOL)purgeAllContact{                         
  return  [alContactDBService purgeAllContact];              
  }                     

  #pragma mark Update APIS                 


  -(BOOL)updateConatct:(ALContact *)contact{               
   return [alContactDBService updateConatct:contact];                
    
   }                    


   -(BOOL)updateListOfContacts:(NSArray *)contacts{                    
   return [alContactDBService updateListOfContacts:contacts];               
   } 


    #pragma mark addition APIS               


   -(BOOL)addListOfContacts:(NSArray *)contacts{              
   return [alContactDBService updateListOfContacts:contacts];                           
   }           

   -(BOOL)addContact:(ALContact *)userContact{                 
    return [alContactDBService addContact:userContact];             
    }         

    #pragma mark fetching APIS                 


    - (ALContact *)loadContactByKey:(NSString *) key value:(NSString*) value{           
    return [alContactDBService loadContactByKey:key value:value];           
    }              


   //-------------------------------------------------------------------------------------------------------         
   // Helper method for demo purpose. This method shows possible ways to insert contact and save it in 
      local database.       
   //-------------------------------------------------------------------------------------------------------     

    - (void) insertInitialContacts{                  

    ALDBHandler * theDBHandler = [ALDBHandler sharedInstance];                       
    
    //contact 1              
    ALContact *contact1 = [[ALContact alloc] init];                       
    contact1.userId = @"adarshk";            
    contact1.fullName = @"Rathan";               
    contact1.displayName = @"Rathan";                
    contact1.email = @"123@abc.com";                
    contact1.contactImageUrl = nil;               
    contact1.localImageResourceName = @"4.jpg";               
    
    // contact 2                 
    ALContact *contact2 = [[ALContact alloc] init];               
    contact2.userId = @"marvel";                  
    contact2.fullName = @"abhishek thapliyal";                
    contact2.displayName = @"abhishek";               
    contact2.email = @"456@abc.com";           
    contact2.contactImageUrl = nil;                  
    contact2.localImageResourceName = @"4.jpg";                      
    
    
    ALContact *contact3 = [[ALContact alloc] init];                   
    contact3.userId = @"don";                 
    contact3.fullName = @"DON";
    contact3.displayName = @"DON";               
    contact3.email = @"don@baba.com";                 
    contact3.contactImageUrl = @"http://tinyhousetalk.com/wp-content/uploads/
    320-Sq-Ft-Orange-Container-Guest-House-00.jpg";    
    contact3.localImageResourceName = nil;                   
    
    //Contact -------- Example with json                             
    
    NSString *jsonString =@"{\"userId\": \"applozic\",\"fullName\": \"Applozic\",
    \"contactNumber\": \"9535008745\",\"displayName\":
    \"Applozic Support\",\"contactImageUrl\": \"https://applozic.com/resources/images/aboutus/rathan.jpg\",
    \"email\":
    \"devashish@applozic.com\",\"localImageResourceName\":null}";                    
    
    ALContact *contact4 = [[ALContact alloc] initWithJSONString:jsonString];                              

   //Contact ------- Example with dictonary                  
    
   NSMutableDictionary *demodictionary = [[NSMutableDictionary alloc] init];                     
   [demodictionary setValue:@"aman999" forKey:@"userId"];               
   [demodictionary setValue:@"aman sharma" forKey:@"fullName"];                 
   [demodictionary setValue:@"aman" forKey:@"displayName"];                  
   [demodictionary setValue:@"aman@applozic.com" forKey:@"email"];                   
   [demodictionary setValue:@"http://images.landofnod.com/is/image
   /LandOfNod/Letter_Giant_Enough_A_231533_LL/$web_zoom$&wid=550&hei=
   550&/1308310656/not-giant-enough-letter-a.jpg"             
   forKey:@"contactImageUrl"];               
   [demodictionary setValue:nil forKey:@"localImageResourceName"];                   
    
   ALContact *contact5 = [[ALContact alloc] initWithDict:demodictionary];                
   [theDBHandler addListOfContacts:@[contact1, contact2, contact3, contact4, contact5]];                                
   }                                                    
  @end                     
 ```          
 
 
 
 
 
  Contact us at ` growth@applozic.com `
 
 
 










   
   
   
   






   
   
   
   
   





























































    


    
  

    










 
 







   









  
  
  
  
   

  
  
  











