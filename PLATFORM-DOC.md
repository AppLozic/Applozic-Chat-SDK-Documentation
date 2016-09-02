Explore Platform API's as per Application Admin or as per Application User.

# HEADERS

###Application Admin

For Application Admin send following authentication headers with each API call to explore platform API's. Request should contain these 3 headers

| Header | Description  |
| ------ | ----------- |
| Apz-AppId | application key got in admin dashboard for which admin want to call api. |
| Apz-Token | Authorization Code. Authentication is done using BASIC authentication. Authorization Code is combination of  base64 value of email & password of  application admin. Basic Base64Encode of "email:password". |
| Content-Type |  application/json  |

**Example**- 
If the email of the admin(Logged in Applozic Dashboard) is  **jack@gmail.com** and password is

| Header | Description  |
| ------ | ----------- |
| Apz-AppId | 21040368s3869d9b2b7b2f953ae28cf |
| Apz-Token | Basic amFja0BnbWFpbC5jb206YWRtaW5Mb2dnZWRJbkFwcGxvemljRGFzaGJvYXJk |
| Content-Type |  application/json  |

###Application User

All request from Device must contain the following 4 headers

| Key | Values  |
| ------------- | ------ |
| Application-Key | Your Application Key |
| Authorization | Authentication is done using BASIC authentication.Basic Base64Encode of userId:deviceKey |
| Device-Key | DeviceKey is received when application user does registration using register/client API. Use Device-Key to create Authorization Code and send Device-Key also in request header.  |
| UserId-Enabled | true |

**Example**- 
If the userId is **robert** and deviceKey is **09c5d869-6d38-4d6b-9ebf-9de16cdab176**, then the authorization code will be:

| Key | Values  |
| ------------- | ------ |
| Application-Key | TestApp |
| Authorization | Basic cm9iZXJ0OjA5YzVkODY5LTZkMzgtNGQ2Yi05ZWJmLTlkZTE2Y2RhYjE3Ng== |
| Device-Key | 09c5d869-6d38-4d6b-9ebf-9de16cdab176 |
| UserId-Enabled | true |

**Note** : Headers are required in each API call except user registration .ie register/client API.

### User API

#### Login/Register User     

**Registration URL**: https://apps.applozic.com/rest/ws/register/client

**Method Type**: POST

**Content-Type**: application/json

**Request body**:  

**json**                         
```
{
  "userId":"robert",
  "deviceType":"4",
  "applicationId":"applozic-sample-app",
  "registrationId":"put-gcm-registration-id-here", 
  "pushNotificationFormat": "0",
  "contactNumber":"+911234567890"
}
```

**Json Parameter Description**:

| Json Parameter  | Required | Default | Description |
| ------------- | ------------- | ------------- | ------------- |       
| userId  | Yes  |   | User name  |
| email  | No  | null  | User email address  |
| password  | No  | null  | User account password  |
| displayName  | No  |   | Name you want to display to other user  |  
| applicationId  | Yes  |   | Your Applozic Application key configured in dashboard  |
| deviceType  | Yes  |   | 1 for Android, 4 for Apple   | 
| registrationId  | No  |   | Device GCM or APN registration id for push notification  | 
| pushNotificationFormat  | No  |   | 0 for Standard (GCM/APN) and 1 for PhoneGap   | 
| userTypeId  | No  |   | to identify different-2 type of user within application  |
| contactNumber  | No  |   | user contact number    |



**Response** : Success Response Json to the request with following properties :-   


**json**
```
{
  "message": "REGISTERED.WITHOUTREGISTRATIONID",
  "userKey": "21fea543-2ade-494f-b905-6bab308d1b4f",
  "deviceKey": "09c5d869-6d38-4d6b-9ebf-9de16cdab176",
  "lastSyncTime": 1454328502029,
  "contactNumber": "+911234567890",
  "currentTimeStamp": 1454328502023
}
```

| Response Parameter  | Description |
| ------------- | ------------- |
| message | One of the following is returned: REGISTERED,REGISTERED.WITHOUTREGISTRATIONID, UPDATED |
| userKey | User key  |
| deviceKey  | User device key |
| lastSyncTime  | Time in miliseconds when user device last synced with server  |  
| contactNumber  | user contact number, received only if passed  | 
| currentTimeStamp  | Time in miliseconds when response is return from server | 


**Note** : **deviceKey** need to be stored and  sent in request header in each API call.

The following will come in response in case of no userId or application key passed:

**json**
```
{
  "message": "INVALID_PARAMETER",
  "currentTimeStamp": 1454328359265
}
```

The following will come in response in case of no application found with the passed application key:

**json** 
```
{
  "message": "INVALID_APPLICATIONID",
  "currentTimeStamp": 1454328359295
}
```
**Note** : No header required for registration API.


#### User Info   

**Display Name  URL**: https://apps.applozic.com/rest/ws/user/info

**Method Type**: GET

**parameters**: 

| Parameter  | Required | Default | Description |
| ------------- | ------------- | ------------- | ------------- |       
| userIds | yes  |  | list of unique userId |

**Note** : Additional **ofUserId**  parameter not required in case of application admin too.

**Example:** For API Call: 

```
http://apps.applozic.com/rest/ws/user/info?userIds=robert&userIds=john&userIds=mark
```

**Response:**

```  
{
  "robert": "robbie",
  "john": "Mitchell"
}
```  
 
**Note**

**1)** Only users having display Name will return in response.


####User Details       

**Note** : API supported both by application admin and application user. No additional parameter **ofUserId** required for Admin.

**URL**: https://apps.applozic.com/rest/ws/user/detail

**Method Type**: GET

**Content-Type**: application/json

**Parameters**:         

| Parameter | Required | Description |
| ------------- |-------  | ------------- |
| userIds |  No    |list of UserId of the user  |
| phoneNumbers | No      |list of phoneNumber of the user  |


**Note** : Pass either userIds or phoneNumbers 

**Response**: 

```
[
 {
  "userId": "UserId1", // UserId of the user (String)
  "userName": "Name1", // Name of the user (String)
  "connected": true, // Current connected status of user, if "connected": true that means user is online (boolean)
  "lastSeenAtTime": 123456789,  // Timestamp of the last seen time of user (long) 
  "imageLink": "http://image.url", // Image url of the user
   "phoneNumber": "+912345678954" // phone number of user
 },
 {
  "userId": "UserId1", // UserId of the user (String)
  "userName": "Name1", // Name of the user (String)
  "connected": true, // Current connected status of user (boolean)
  "lastSeenAtTime": 123456789,  // Timestamp of the last seen time of user (long) 
  "imageLink": "http://image.url" // Image url of the user
 }
]
```

#### Update User

**UPDATE User URL**: https://apps.applozic.com/rest/ws/user/update 

**Method Type**: POST

**ContentType**: application/json

**Request Body**:  

**json**                         
```
{
  { "email" : "user email",
  "displayName" : "user display name",
  "imageLink" : "User profile image url",
  "statusMessage": "status Message"
 }
}
```
**Json Parameter Description** 

|Json Parameter  | Required | Default  | Description |
| ------------- | ------------- | ------------- | ------------- |
| email   | No  |   | user email  |
| displayName | No  |   | display name of user |
| imageLink | No  |   | image link of the user |
| statusMessage | No  |   | status message of user |


**Note**: Pass **ofUserId** only if application Admin calling the API.

**Request Parameter**: 

| Parameter  | Required | Default  | Description |
| ------------- | ------------- | ------------- | ------------- |
| ofUserId  | Yes (in case of admin only) |   |pass userId of user for which admin want to update details.  |

**Response**: Response Json with success status :-  

```  
{
  "status": "success",
  "generatedAt": 1452347180639,  // time value at which response is generated from server
  "response": "success"
}
```


#### Update User Password  

**Update Password  URL**: https://apps.applozic.com/rest/ws/user/update/password

**Method Type**: GET

**parameters**: 

| Parameter  | Required | Default | Description |
| ------------- | ------------- | ------------- | ------------- |       
| oldPassword | yes  |  | existing password |
| newPassword | yes  |  | new password |



**Example:** For API Call: 

```
http://apps.applozic.com/rest/ws/user/update/password?oldPassword=12345&newPassword=1234567
```

**Response:**

```  
{
  "status": "success",
  "generatedAt": 1452347180639,  // time value at which response is generated from server
  "response": "success"
}
``` 




####User Exist

**Note** : API supported both by application admin and application user. No additional parameter **ofUserId** required for Admin.

**URL**: https://apps.applozic.com/rest/ws/user/exist

**Method Type**: GET

**Content-Type**: application/json

**Parameters**:         

| Parameter | Required | Description |
| ------------- |-------  | ------------- |
| userId | Yes | UserId of the user  |

**Response**: 

```
If Web user : "web user"
If Android : version code of the device
If Not Found : "User Not Found"
```

#####Contact List   

**CONTACT LIST URL**: http://apps.applozic.com/rest/ws/user/filter

**Method Type**: GET

**parameters**: 

| Parameter  | Required | Default | Description |
| ------------- | ------------- | ------------- | ------------- |       
| pageSize | No  | 500 | list of contacts to load |
| startTime | No  |  | pass to load more contact |
| userId  | No  |   | pass userId of user for which information has to be retrieved |
| role  | No  |   | pass role of users for which information has to be retrieved |


Roles:

| Parameter  |
| ------------- |
| BOT |
| USER |

**Example:** For API Call: 

```
http://apps.applozic.com/rest/ws/user/filter?pageSize=20
```

**Response:**

```  
{
  "users": [
    {
      "userId": "mark",
      "connected": false,
      "lastSeenAtTime": 1461559344000,
      "createdAtTime": 1461559342000,
      "unreadCount": 0,
      "deactivated": false
    },
    {
      "userId": "john",
      "connected": true,
      "lastSeenAtTime": 1460801797000,
      "createdAtTime": 1460803509000,
      "unreadCount": 0,
      "displayName": "Edward",
      "deactivated": false
    },
    {
      "userId": "chris",
      "connected": true,
      "createdAtTime": 1460803509000,
      "unreadCount": 0,
      "displayName": "adam",
      "imageLink": "https://www.applozic.com/resources/images/applozic_logo.gif",
      "deactivated": false
    }
    (20 users detail list...)
  ],
  "lastFetchTime": 1460803509000,
  "totalUnreadCount": 0
}
```  

**Note** : To load further contact list use **lastFetchTime** value and pass it in **startTime** parameter from next time onwards.

###Message API

#### Send Message

**Note** : API supported both by application admin and application user.

**SEND MESSAGE URL**: https://apps.applozic.com/rest/ws/message/send

**Method Type**: POST

**Content-Type**: application/json

**Request Body**:

**Note** : Request body in case of **One to One message send**. 

**Json**                         
```
{
  "to":"John",
  "message":"Hi John"
}
```

**Json Parameter Description**: 

| Json Parameter  | Required | Default  | Description |
| ------------- | ------------- | ------------- | ------------- |
| to  | Yes  |   | UserId to which you want to send message |
| message  | Yes  |   | Text Message |




**Note** : Request body in case of **Group message send**. 

**Json**                         
```
{
 "clientGroupId": "group Unique Identifier",  
  "message":"Hi John"
}
```


**Json Parameter Description**:

| Json Parameter  | Required | Default  | Description |
| ------------- | ------------- | ------------- | ------------- |
| clientGroupId  | Yes  |   | Unique identifier of the group with respect to client |
| message  | Yes  |   | Text Message |




**Note** : In case of Application Admin  **ofUserId** request param required too.

**Request Parameter**: 

| Parameter  | Required | Default  | Description |
| ------------- | ------------- | ------------- | ------------- |
| ofUserId  | Yes (in case of admin only) |   |pass userId of user on which behalf admin want to create group    |

**Response** Same in both case: **One to One** and **Group Message Send**

**Json**
```
{
  "messageKey": "5-22bf4626-9019-4a4a-8565-6c0e40ecda96-1454398305364",
  "createdAt": 1454398305000
}
```

| Response Parameter  | Description |
| ------------- | ------------- |
| message key  | Request is successfully processed  |
| createdAt  | time in milliseconds |

#### Broadcast Message

**URL**: https://apps.applozic.com/rest/ws/message/sendall

**Method Type**: POST

**Content-Type**: application/json

**Request Body** :  

**Json**
```
{
  "userNames" : ["UserName1", "UserName2", "UserName3"],
  "clientGroupIds" : ["1", "2", "3"],
  "messageObject" : {
    "message":"Hi John"
  }
}
```

**Json Parameter Description**:

| Json Parameter  | Required | Default  | Description |
| ------------- | ------------- | ------------- | ------------- |
| userNames  | No  |   | User Names to which you want to send message |
| clientGroupIds  | No  |   | List of Group unique identifiers to which you want to send message |
| messageObject  | Yes  |   | Message Container Object |
| message  | Yes  |   | Text Message |

**Note** : In case of Application Admin  **ofUserId** request param required too.

**Request Parameter**: 

| Parameter  | Required | Default  | Description |
| ------------- | ------------- | ------------- | ------------- |
| ofUserId  | Yes (in case of admin only) |   |pass userId of user on which behalf admin want to create group    |



**Response** : success Response Json to the request

####Message list

**URL**: https://apps.applozic.com/rest/ws/message/list

**Method Type**: GET

**Description**

1. If no user id or group id is passed to the api then this api returns the latest message of the calling user with each user or group which the user has chat with.
2. If the user id or group id is passed then api return the messages between the calling user and specified user.
3. If the group id is passed the api returns the messages of the specified group.

**Request Body**:        

| Parameter  | Required | Default  | Description |
| ------------- | ------------- | ------------- | ------------- |
| userId  | No  |  | User Id of the user whose respective chat messages user want to fetch.  | 
| groupId  | No  |  | Group Id of the group for which messages need to be fetched. | 
| startIndex  | Yes  | 0  | Starting Index to fetch messages from list.  | 
| pageSize  | Yes  | 50  | Number of messages per page you want to fetch.  |
| startTime  | No  |   | Start Time from when you want to fetch message list. It is number of milliseconds since January 1, 1970, 00:00:00 GMT |
| endTime  | No  |   | End Time upto when you want to fetch message list. It is number of milliseconds since January 1, 1970, 00:00:00 GMT |
| ofUserId  | No  |   |pass userId of user on behalf of which application admin want to call API |

**Note** : Pass **ofUserId** only if application Admin calling the API on behalf of any user.

**Note** : For fetching the next page of your message list startIndex value should be equal to the sum of pageSize value of all the previous calls.

**Response**:
```  
{
  "message":[
    {
      "key":"5-35c2957b-8de0-482b-bea9-7c5c2e1dd2f4-1452080064726",
      "userKey":"35c2957b-8de0-482b-bea9-7c5c2e1dd2f4",
      "to":"michael",
      "contactIds":"michael",
      "message":"how are you",
      "sent":true,
      "delivered":false,
      "read":false,
      "createdAtTime":1452080064000,
      "type":5,
      "source":1,
      "status":3,
      "pairedMessageKey":"4-35c2957b-8de0-482b-bea9-7c5c2e1dd2f4-1452080064726",
      "contentType":0
    }
  ]
}      
```

**In Case of Error** :

| Response  | Description | 
| ------------- | ------------- | 
| error  | In case of any exception or error contact resolve@applozic.com  |


#### Delete Message     

**DELETE MESSAGE  URL**: https://apps.applozic.com/rest/ws/message/delete

**Method Type**: GET 

**Parameters**:

| Parameter  | Required | Default  | Description |
| ------------- | ------------- | ------------- | ------------- |
| key  | Yes  |   | Message unique key  |
| ofUserId  | No  |   |pass userId of user for which admin to delete message |

**Note** : Pass **ofUserId** only if application Admin calling the API on behalf of any user.

**Response**:        

| Parameter  | Description | 
| ------------- | ------------- | 
| success  | Request is successfully processed  |
| error  |This will come if any exception occurs on server. In case of any exception contact resolve@applozic.com  |


#### Delete Conversation           

**DELETE CONVERSATION  URL** : https://apps.applozic.com/rest/ws/message/delete/conversation

**Method Type**: GET 

**Parameters**:          

| Parameter  | Required | Default  | Description |
| ------------- | ------------- | ------------- | ------------- |
| userId  | No  |   | User for which you want to delete thread  |  
| groupId  | No  |   | Group for which you want to delete thread  |  
| ofUserId  | No  |   |pass userId of user on behalf of which application admin want to call API |

**Note** : Pass **ofUserId** only if application Admin calling the API on behalf of any user.

**Note** :

**1)** For Delete Conversation in Group send **groupId**  as a parameter.

**2)** For Delete Conversation in One to One Chat send **userId**  as a parameter.

**Response**:           

| Parameter  | Description | 
| ------------- | ------------- | 
| success  | Request is successfully processed  |
| error  |This will come if any exception occurs on server or all the parameters are null. In case of any exception contact resolve@applozic.com  |

#### Delete All Chats         

**DELETE All  URL** : https://apps.applozic.com/rest/ws/message/delete/all

**Method Type**: GET

**Note** : Request param **ofUserId** required for application admin purpose only.

**Parameters**:          

| Parameter  | Required | Default  | Description |
| ------------- | ------------- | ------------- | ------------- |
| ofUserId  | No  |   | User for which application admin want to delete all messages  |  

**Response**:           

| Parameter  | Description | 
| ------------- | ------------- | 
| success  | Request is successfully processed  |
| error  |This will come if any exception occurs. In case of any exception contact reslove@applozic.com  |


####Message Metadata

To add metadata for a message, send the metadata object inside the message object while sending message. The same metadata object will be received in message list api with message objet. The metadata object is a map with string keys and values.

**Sample Message Object Json with Metadata**:          

```json
{
  "to":"John",
  "message":"Hi John",
  "metadata" : {
    "key1" : "value1",
    "key2" : "value2"
  }
}
```

### Group API

#### Create Group

**GROUP CREATION URL**: https://apps.applozic.com/rest/ws/group/v2/create 

**Method Type**: POST 

**ContentType**: application/json


**Request Body**:   

**Json**  
```
{
  "clientGroupId":"Client Group Id",  // optional
  "groupName" : "Group Name",
  "groupMemberList" : ["UserName1", "UserName2", "UserName3"]
}
```
**Json Parameter Description**: 

| Json Parameter  | Required | Default  | Description |
| ------------- | ------------- | ------------- | ------------- |
| clientGroupId | No  |   | Unique identifier of the group with respect to client |
| groupName | Yes  |   | Name of the group |
| groupMemberList | Yes  |   |List of userIds of the  group members |
| type | No  | public  | Type of the group |

**Note** : 

**1)** If group already exist in your system, pass that group unique identifier in **clientGroupId** to use the same with Applozic.

**2)** If **clientGroupId** is not passed then Applozic will generate a unique id for the group which should be used as **clientGroupId** for all API calls.

"type" parameters possible values

| Value  | Description |
| ------------- | ------------- |
| 1 | Private group : Other users are not able to join this group voluntarily |
| 2 | Public Group : Users are able to search and join the group |
| 5 | Broadcast Group : User can send personal message to a group of Users |
| 6 | Open Group : Any user can send the message to this group without being the member of this group |


**Note** : In case of Application Admin  **ofUserId** request param required too.

**Request Parameter**: 

| Parameter  | Required | Default  | Description |
| ------------- | ------------- | ------------- | ------------- |
| ofUserId  | Yes (in case of admin only) |   |pass userId of user on which behalf admin want to create group    |
 




**Response** : Response Json  with success status :-  

```json
{
  "status": "success",
  "generatedAt": 1464854985171,  // time value at which response is generated from server
  "response": {
    "id": 274457,
    "clientGroupId": "Client Group Id",
    "name": "Group Name",
    "adminId": "TestUser",
    "membersId": [
      "UserName2",
      "UserName3",
      "UserName1",
      "TestUser"
    ],
    "users": [
      {
        "id": "77749a25-b260-4e37-aa62-12b8dfc64657",
        "userId": "UserName2",
        "connected": false,
        "createdAtTime": 1464854985050,
        "unreadCount": 0,
        "deactivated": false
      },
      {
        "id": "05c576da-538d-4f46-aa34-8ba4bccf98f0",
        "userId": "UserName3",
        "connected": false,
        "createdAtTime": 1464854985057,
        "unreadCount": 0,
        "deactivated": false
      },
      {
        "id": "894591fc-a48a-4e0a-ae9b-fd5125002f46",
        "userId": "UserName1",
        "connected": false,
        "createdAtTime": 1464854985062,
        "unreadCount": 0,
        "deactivated": false
      }
    ],
    "unreadCount": 0,
    "type": 2
  }
}
```

#### Multiple Group Creation

**MULTIPLE GROUP CREATION URL**: https://apps.applozic.com/rest/ws/group/v2/create/multiple

**Method Type**: POST 

**ContentType**: application/json

**Request Body**: 

**Json**  
```
[
  {
    "clientGroupId": "GroupId1",  //optional
    "groupName" : "MultiGroup1",
    "groupMemberList" : [ "kevin","john"]
  },
  {
    "groupName" : "MultiGroup2",
    "groupMemberList" : [ "jade"]
  }
]
```

**Json Parameter Description**:

| Json Parameter  | Required | Default  | Description |
| ------------- | ------------- | ------------- | ------------- |
| clientGroupId | No  |   | Unique identifier of the group with respect to client |
| groupName | Yes  |   | Name of the group |
| groupMemberList | Yes  |   |List of userIds of the  group members |
| type | No  | public  | Type of the group |

**Note** : 

**1)** If group already exist in your system, pass that group unique identifier in **clientGroupId** to use the same with Applozic.

**2)** If **clientGroupId** is not passed then Applozic will generate a unique id for the group which should be used as **clientGroupId** for all API calls.

"type" parameters possible values

| Value  | Description |
| ------------- | ------------- |
| 1 | Private group : Other users are not able to join this group voluntarily |
| 2 | Public Group : Users are able to search and join the group |
| 5 | Broadcast Group : User can send personal message to a group of Users |

**Note** : In case of Application Admin  **ofUserId** request param required too.

**Request Parameter**: 

| Parameter  | Required | Default  | Description |
| ------------- | ------------- | ------------- | ------------- |
| ofUserId | Yes (in case of admin only) | |pass userId of user on which behalf admin want to create  multiple group |




**Response** : Response Json  with success status :-  

**json**                         
```
{
  "status": "success",
  "generatedAt": 1464793892242,  // time value at which response is generated from server
  "response": [
    {
      "id": 496,
      "clientGroupId": "GroupId1",
      "name": "MultiGroup1",
      "adminId": "TestUser",
      "membersId": [
        "kevin",
        "TestUser",
        "john"
      ],
      "users": [
        {
          "id": "1d18ac83-5e00-4663-bdb8-91cc1354b63d",
          "userId": "John",
          "connected": false,
          "createdAtTime": 1457714415000,
          "unreadCount": 0,
          "deactivated": false
        },
        {
          "id": "8bb2f211-1083-4032-8187-5bc6db1c2080",
          "userId": "kevin",
          "connected": true,
          "lastSeenAtTime": 1457449548000,
          "createdAtTime": 1457449539000,
          "unreadCount": 0,
          "phoneNumber": "+912345678923",
          "deactivated": false
        }
      ],
      "unreadCount": 0,
      "type": 2
    },
    {
      "id": 497,
      "clientGroupId": "497", // same as Applozic group Id.
      "name": "MultiGroup2",
      "adminId": "TestUser",
      "membersId": [
        "TestUser",
        "jade"
      ],
      "users": [
        {
          "id": "39fcf05f-572d-4efb-8e34-8a4004f1bb37",
          "userId": "jade",
          "connected": false,
          "createdAtTime": 1464681811000,
          "unreadCount": 0,
          "deactivated": false
        }
      ],
      "unreadCount": 0,
      "type": 2
    }
  ]
}
```

#### Group Info

**LIST URL**:  https://apps.applozic.com/rest/ws/group/v2/info 

**Method Type**: GET

**Parameters**:        

| Parameter  | Required | Default  | Description |
| ------------- | ------------- | ------------- | ------------- |
| groupId | No  |   | Group Id of the group  |
| clientGroupId  | No  |   | Client Group id of the group |

**Response**:   Response Json with success status :-
```
{
  "status": "success",
  "generatedAt": 1465310497564,
  "response": {
      "id": 496,
      "clientGroupId": "GroupId1",
      "name": "MultiGroup1",
      "adminId": "TestUser",
      "membersId": [
        "kevin",
        "john",
        "TestUser"
      ],
      "removedMembersId": [],
      "unreadCount": 0,
      "type": 2
    }
}
```

#### User's Group List

**LIST URL**:  https://apps.applozic.com/rest/ws/group/v2/list 

**Method Type**: GET

**Parameters**:        

| Parameter  | Required | Default  | Description |
| ------------- | ------------- | ------------- | ------------- |
| updatedAt | No  |   | lastSyncTime to the server  |
| ofUserId  | No  |   |pass userId of user for which admin want to load the group list   |

**Note** : Pass **ofUserId** only if application Admin calling the API on behalf of any user.

**Response**:   Response Json with success status :-         

```
{
  "status": "success",
  "generatedAt": 1465310497564,    // time value at which response is generated from server
  "response": [
    {
      "id": 496,
      "clientGroupId": "GroupId1",
      "name": "MultiGroup1",
      "adminId": "TestUser",
      "membersId": [
        "kevin",
        "john",
        "TestUser"
      ],
      "removedMembersId": [],
      "unreadCount": 0,
      "type": 2
    },
    {
      "id": 497,
      "clientGroupId": "497",
      "name": "MultiGroup2",
      "adminId": "TestUser",
      "membersId": [
        "jade",
        "TestUser"
      ],
      "removedMembersId": [],
      "unreadCount": 0,
      "type": 2
    }
  ]
}
```

**Note**: For the next sync call, pass "updatedAt" parameter to get details of only the modified group and newly added group of that user. Applozic API response contains "generatedAt" parameter which contains the timestamp at the time of server response. Use it as "updatedAt" for your next sync call.


#### Add User to Group

**ADD GROUP MEMBER URL**:  https://apps.applozic.com/rest/ws/group/add/member 

**Method Type**: GET

**Parameters**: 

| Parameter  | Required | Default  | Description |
| ------------- | ------------- | ------------- | ------------- |
| clientGroupId   | Yes  |   | Group unique identifier  |
| userId   | Yes  |   | Name of the user want to add to the group  |
| ofUserId  | No  |   | Pass userId of user on behalf of which application admin want to add member  |

**Note** : Pass **ofUserId** only if application Admin calling the API on behalf of any user.

**Response**:  Response Json with success status :-  

```  
{
  "status": "success",
  "generatedAt": 1452347180639, // time value at which response is generated from server
  "response": "success"
}
```


#### Add users to Many Groups

**URL**:  https://apps.applozic.com/rest/ws/group/add/users

**Method Type**: GET

**Parameters**: 

| Parameter  | Required | Default  | Description |
| ------------- | ------------- | ------------- | ------------- |
| clientGroupIds   | Yes  |   | List of Group unique identifiers  |
| userIds   | Yes  |   | List of Unique ids of the users to be added to the group  |
| ofUserId  | No  |   | Pass userId of user on behalf of which application admin want to add member  |

**Note**: Pass **ofUserId** only if application Admin calling the API on behalf of any user.



**Response**:  Response Json with success status :-  
```  
{
  "status": "success",
  "generatedAt": 1452347180639, // time value at which response is generated from server
  "response": "success"
}
```

**Note**: Groups for the passed clientGroupIds and the user for the passed userId should exist in that application.


### Remove User from Group 

**REMOVE GROUP MEMBER URL**:  https://apps.applozic.com/rest/ws/group/remove/member 

**Method Type**: GET

**Parameters**: 

| Parameter  | Required | Default  | Description |
| ------------- | ------------- | ------------- | ------------- |
| clientGroupId   | Yes  |   | Group unique identifier  |
| userId   | Yes  |   | UserId of the user want to remove from group  |
| ofUserId  | No  |   | Pass userId of user on behalf of which application admin want to remove member |

**Note**: Pass ofUserId only if application Admin calling the API on behalf of any user.

**Response**:  Response Json  with success status :-  

```  
{
  "status": "success",
  "generatedAt": 1452347180639, // time value at which response is generated from server
  "response": "success"
}
```

**Note**: Only Admin can remove the group member from private group otherwise the following error will come:

```  
{
  "status":"error",
  "errorResponse":[
    {
      "errorCode":"AL-UN-01",
      "description":"unauthorized user",
      "displayMessage":"Unable to process"
    }
  ],
  "generatedAt":1452348983616  // time value at which response is generated from server
}
```



#### Leave Group

**LEAVE GROUP URL**:  https://apps.applozic.com/rest/ws/group/left 

**Method Type**: GET

**Parameters**: 

| Parameter  | Required | Default  | Description |
| ------------- | ------------- | ------------- | ------------- |
| clientGroupId   | Yes  |   | Group unique identifier  |
| ofUserId  | No  |   | Pass userId of user application admin want to remove |

**Note**: Pass **ofUserId** only if application Admin calling the API on behalf of any user.

**Response**: Response Json with success status :-  

```  
{
  "status": "success",
  "generatedAt": 1452347180639,  // time value at which response is generated from server
  "response": "success"
}
```



#### Update Group

**UPDATE GROUP URL**: https://apps.applozic.com/rest/ws/group/update 

**Method Type**: POST

**ContentType**: application/json

**Request Body**:  

| Parameter  | Required | Default  | Description |
| ------------- | ------------- | ------------- | ------------- |
| clientGroupId   | Yes  |   | Group unique identifier  |
| newName | No  |   | New name of group |
| imageUrl | No  |   | image url of the group |
| ofUserId  | No  |   | Pass userId of user on behalf of which application admin want to change group name |

**Note**: Pass **ofUserId** only if application Admin calling the API on behalf of any user.

**Response**: Response Json with success status :-  

```  
{
  "status": "success",
  "generatedAt": 1452347180639,  // time value at which response is generated from server
  "response": "success"
}
```

#### Group - Is User Present
Check if user is part of a Group

**CHECK USER URL**:  https://apps.applozic.com/rest/ws/group/check/user 

**Method Type**: GET

**Parameters**: 

| Parameter  | Required | Default  | Description |
| ------------- | ------------- | ------------- | ------------- |
| clientGroupId   | Yes  |   | Group unique identifier  |
| userId   | Yes  |   | UserId of the user identify in group  |
| ofUserId  | No  |   | Pass userId of user exist in a group on behalf of which application admin want to check other user |

**Note**: Pass **ofUserId** only if application Admin calling the API on behalf of any user.

**Response**:  API response: in case of success :-  

```  
{
  "status": "success",
  "generatedAt": 1463673355057,  // time value at which response is generated from server
  "response": true/false
}
```

#### Group Users Count 

**URL**:  https://apps.applozic.com/rest/ws/group/user/count

**Method Type**: GET

**Parameters**: 

| Parameter  | Required | Default  | Description |
| ------------- | ------------- | ------------- | ------------- |
| clientGroupIds   | Yes  |   | List of Group unique identifiers  |


**Response**:  Response Json with success status :-  
```  
{
  "status": "success",
  "generatedAt": 1469293877608,
  "response": [
    {
      "id": 503,
      "clientGroupId": "503",
      "userCount": 3
    },
    {
      "id": 504,
      "clientGroupId": "clientGroupId",
      "userCount": 5
    }
  ]
}
```

### Group Delete 

**DELETE GROUP URL**:  https://apps.applozic.com/rest/ws/group/delete 

**Method Type**: GET

**Parameters**: 

| Parameter  | Required | Default  | Description |
| ------------- | ------------- | ------------- | ------------- |
| clientGroupId   | Yes  |   | Group unique identifier  |
| ofUserId  | No  |   | Pass userId of group admin user, for which application admin want to delete the group   |

**Note**: Pass **ofUserId** only if application Admin calling the API on behalf of group admin user.

**Response**:  Json with success status :-  

```
{
  "status": "success",
  "generatedAt": 1463673355057,  // time value at which response is generated from server
  "response": true
}  
```

**Note**: Only Group Admin can delete the group otherwise the following error will come:

```
{
  "status":"error",
  "errorResponse":[
    {
      "errorCode":"AL-UN-01",
      "description":"unauthorized user",
      "displayMessage":"Unable to process"
    }
  ],
  "generatedAt":1452348983616   // time value at which response is generated from server
}
```

#### Channel (or Group)

**URL**:  https://apps.applozic.com/rest/ws/group/channel 

**Method Type**: GET

**Parameters**: 

| Parameter  | Required | Default  | Description |
| ------------- | ------------- | ------------- | ------------- |
| pageSize  | Yes  | 50  | Number of messages per page you want to fetch.  |
| startTime  | No  |   | Start Time from when you want to fetch message list. It is number of milliseconds since January 1, 1970, 00:00:00 GMT.  |
| endTime  | No  |   | End Time upto when you want to fetch message list. It is number of milliseconds since January 1, 1970, 00:00:00 GMT.  |

**Response**:  Json with success status :-  

```
{
  "status": "success",
  "generatedAt": 1465310497564,    // time value at which response is generated from server
  "response": [
    {
      "id": 496,
      "clientGroupId": "GroupId1",
      "name": "MultiGroup1",
      "adminId": "TestUser",
      "membersId": [
        "kevin",
        "john",
        "TestUser"
      ],
      "removedMembersId": [],
      "unreadCount": 0,
      "type": 6
    },
    {
      "id": 497,
      "clientGroupId": "497",
      "name": "MultiGroup2",
      "adminId": "TestUser",
      "membersId": [
        "jade",
        "TestUser"
      ],
      "removedMembersId": [],
      "unreadCount": 0,
      "type": 6
    }
  ]
}
```


### Contextual (Topic/Product) Chat 

#### Conversation Id

Retreive Conversation Id

**URL**: https://apps.applozic.com/rest/ws/conversation/id

**Method Type**: POST

**Content-Type**: application/json

**Request Body**:
```
{
  "topicId" : "Topic id of the conversation",
  "topicDetail" : "Topic detail of the conversation",
  "applicationKey" : "Application key",
  "userId" : "unique id of the receiver user", // or "groupId": "groupId  receive from group creation API"
  "status" : "Status flag of the conversation"
}
```

**Note**

1.In case of One to One chat  pass **userId**  and in case of group chat pass **groupId** in request body.

**Behavior**

1. Call retrieve conversation API with Status flag as NEW, OPEN, DEFAULT.

2. If no conversation is found, new conversation will be created.

Status Behavior

NEW: The previous conversation will get ended and new conversation will be created.

OPEN: If the conversation is closed, it will be re-opened.

DEFAULT: return the conversation as it is.

***Required Authentication Headers***

**request should contain these 3 headers** -

| Header | Value |
| ------------- | ------------ |
| Key | Values  |
| UserId-Enabled | true |
| Application-Key | Your Application Key  |  
| Device-Key | Received in registration response  | 

Authentication is done using BASIC authentication. It is combination of email & password of admin user .

**Response**:  success Response Json to the request
```
{
  "status" : "success",
  "response" : {
    "id" : Group Id (integer),
    "name" : "Group Name",
    "adminId" : "Group Admin User Name",
    "membersId" : [ List of members user names],
    "unreadCount" : (Int) message unread count for the logged in user,
    "type" : Group type,
    "conversationPxy" : {
      "id" : (Int)Conversation id,
      "topicId" : "Topic id of the conversation",
      "topicDetail" : "Topic Detail for the conversation",
      "created" : (true/false) if the conversation is created or not in this api,
      "closed" : (true/false) if the conversation is closed,
      "groupId" : (Int) Group id of the respected group,
    }
  }
}
```

### Block/Unblock API

#### Block User     

**BLOCK USER  URL**: https://apps.applozic.com/rest/ws/user/block

**Method Type**: GET 

**Parameters**:         

| Parameter  | Required | Default  | Description |
| ------------- | ------------- | ------------- | ------------- |
| userId | Yes  |   |pass unique id of user you want to block  |

**Response**:  Response Json with success status :-  

```
{
  "status": "success",
  "generatedAt": 1463673355057,  // time value at which response is generated from server
  "response": true
}   
```

#### Unblock User    

**UNBLOCK USER  URL**: https://apps.applozic.com/rest/ws/user/unblock

**Method Type**: GET 

**Parameters**:         

| Parameter  | Required | Default  | Description |
| ------------- | ------------- | ------------- | ------------- |
| userId | Yes  |   |pass unique id of user you want to unblock  |

**Response**:  Response Json with success status :-  

```  
{
  "status": "success",
  "generatedAt": 1463673355057,  // time value at which response is generated from server
  "response": true
}  
``` 

### Application Admin APIs
API's for application admin purpose only

**Application To User**

Application can send automated in-app messages to users using Application to User Messaging API.

**Note** : Send authentication headers in API call required by Application Admin.

#### Create User        

**URL**: https://apps.applozic.com/rest/ws/user/v2/create

**Method Type**: POST

**Content-Type**: application/json

**Request Body**:

**Json**
```
{
  "userId": "DemoUser", 
  "displayName": "Display Demo User Name", 
  "imageLink": "User profile image url", 
  "email": "User Email", 
  "createdAtTime": 1456148218000, // if want to create user on specific time
   "roleName":"BOT" // if want to create application Bot user
}
```

**Json Parameter Description**:

| Json Parameter  | Required | Default  | Description |
| ------------- | ------------- | ------------- | ------------- |
| userId | Yes  |   |pass unique id of user  |
| displayName | No  |   |display name of user  |
| imageLink | No |   |image link of user  |
| email | No  |   |email of user  |
| createdAtTime | No  |   |time in miliseconds  |
| roleName | No  |   | want to create user of specific type: BOT  |




**Response**: 

```
{
  "status": "success",
  "generatedAt": 1470903020662,
  "response": "success"
}
```



#### Update User Password  

**Update User Password  URL**: https://apps.applozic.com/rest/ws/user/update/password/by/admin

**Method Type**: GET

**parameters**: 

| Parameter  | Required | Default | Description |
| ------------- | ------------- | ------------- | ------------- |       
| userId | yes  |  | unique identifier for user |
| password | yes  |  |  password for user |



**Example:** For API Call: 

```
http://apps.applozic.com/rest/ws/user/update/password?userId=jack&password=1234567
```

**Response:**

```  
{
  "status": "success",
  "generatedAt": 1452347180639,  // time value at which response is generated from server
  "response": "success"
}
``` 



#### Merge Users

**Note** : API supported only by application admin. No additional parameter **ofUserId** required for Admin.

**URL**: https://apps.applozic.com/rest/ws/user/merge?userId=user1&mergeUserId=user2

**Method Type**: GET

**Content-Type**: application/json

**Parameters**:         

| Parameter | Required | Description |
| --------- | -------  | ----------- |
| userId |  Yes | UserId of the user in which data will be merged  |
| mergeUserId | Yes | UserId of the user which will be merged  |

**Response**:           

| Parameter  | Description | 
| ------------- | ------------- | 
| success | Request is successfully processed  |
| error |This will come if any exception occurs on server or all the parameters are null. In case of any exception contact resolve@applozic.com  |

###Dispatch Message   

**DISPATCH MESSAGE URL**: https://apps.applozic.com/rest/ws/message/dispatch

**Description** : 

1.Message Dispatch API behave same as Message Send API, but used by Application Admin.

2.Message Dispatch API supports One to One, group based and contextual based messaging.

3.Application Admin can send Message on behalf of one user to another user on back date also. (Used for data migration from your Server to Applozic Sever)

**Method Type**: POST

**Content-Type**: application/json

**Request body**:  

**Json required for One to One based messaging**:

**json**
```
{
  "message":"HI STEVE",
  "senderName":"john",
  "to": "steve"   
}

```

**Json Parameter Description**:

|Json Parameter  | Required | Default | Description |
| ------------- | ------------- | ------------- | ------------- |       
| senderName | Yes  |   | unique Id of  message sender user  |
| to | Yes  |   | unique Id of message receiver user  |
| message  | Yes |   | message content to be passed  |
| oldTimestamp  | No |   | create message  timestamp   |



**Response**:



**Json**
```
{
  "messageKey": "5-a97d66cd-67f9-42ba-aa61-a357455088ac-1456148218362",
  "createdAt": 1456148218000
}
```

| Response Parameters  | Description |
| ------------- | ------------- |
| messageKey |message key  |
| createdAt | Time in miliseconds when response is return from server |

**Json required for group based messaging**:

**json**
```
{
  "message":"message content",
  "groupId":114209 //groupId received while group creation.
}
```

**Response**:



**Json**
```
{
  "messageKey": "5-agpzfmFwcGxvemljchMLEgZTdVVzZXIYgICAgLrcvwsM-1464093115599",
  "createdAt": 1456148218000
}
```

| Response Parameters  | Description |
| ------------- | ------------- |
| messageKey |message key  |
| createdAt | Time in miliseconds when response is return from server |

**Json required for contextual based messaging**:

**json**
```
{
  "message":"Hello, I am interested in the product, can we chat?",
  "senderName":"john",
  "to": "steve",
  "conversationPxy": {
    "topicId":"prodct topic Id",
    "topicDetail": "topic detail string"    
  }   
}
```

**Response**:      



**json**
```
{
  "messageKey":"5-a97d66cd-67f9-42ba-aa61-a357455088ac-1458039322283",
  "conversationId":456,
  "createdAt":1458039322000
}
```

| Response Parameters  | Description |
| ------------- | ------------- |
| messageKey |message key  |
| createdAt | Time in miliseconds when response is return from server |
| conversationId | open conversation to chat on topic |

#### Message History Export

**Note** : API supported only by application admin. No additional parameter **ofUserId** required for Admin.

**URL**: https://apps.applozic.com/rest/ws/analytics/message

**Method Type**: GET

**Content-Type**: application/json

**Accept**:

1. application/json (Default) : For return type as json
2. application/octet-stream : For returning as Excel.

**Parameters**:         

| Parameter | Required | Description |
| --------- | -------  | ----------- |
| applicationId | Yes | Your Applozic Application key configured in dashboard |
| startIndex | No | Starting Index to fetch messages from list |
| pageSize | No | Number of messages per page you want to fetch |
| from | No | UserId of the sender for the fetched message |
| to | No | UserId of the receiver for the fetched message |
| startTime | No | Start Time from when you want to fetch message list. It is number of milliseconds since January 1, 1970, 00:00:00 GMT |
| endTime | No | End Time upto when you want to fetch message list. It is number of milliseconds since January 1, 1970, 00:00:00 GMT |
| messageType | No | Message type of the message to check |
| period | No | if startTime is not passed. amount of period to check the message |
| timeUnit | No | Time unit of the period |

messageType : Possible Values:

1. MessageDelivered
2. MessageUnDelivered
3. MessageRead
4. MessageUnRead

timeUnit : Possible Values:

1. MilliSeconds
2. Second
3. Minute
4. Hour
5. Day
6. Week
7. Month
8. Year

**Response**:           

**Response**:  Response Json with success status :-  

```  
{
  "status": "success",
  "generatedAt": 1463673355057,  // time value at which response is generated from server
  "response": [
    {
      "id" : "5-agpzfmFwcGxvemljchMLEgZTdVVzZXIYgICAgLrcvwsM-1464093115599",
      "fromUserId" : "john",
      "toUserId" : "steve",
      "groupName" : null,
      "content" : "Hello",
      "createdAtTime" : 1458039322000,
      "deliveredAtTime" : 1458039322000,
      "readAtTime" : 1458039322000
    }
  ]
}  
```

Contact us at ` github@applozic.com `
