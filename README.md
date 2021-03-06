# NOTE: For manually testing, please add ?debug=true at the end each request made to get full info.
# dropin-doc


## [Registration](#Registration)

* [Create new account](#new_account)

## [Authorization](#Authorization)

* [Login](#login)
* [Verify](#verify)
* [Logout](#logout)

## [Device](#Device)

* [Add new device](#new_device)

## [Notification](#Notification)

* [Send notification](#send_notification)
* [Mark a notification as read](#mark_notification_read)
* [Get list of unread notification](#get_unread_list_notification)
* [Get list of notification](#get_list_notification)
* [Get notification](#get_notification)
* [Remove notification](#remove_notification)

## [Profile](#Profile)
* [Get account profile](#get_account_profile)
* [Update account profile](#update_account_profile)
* [Deactivate account](#deactivate_account)

## [Setting](#Setting)
* [Get account setting](#get_account_setting)
* [Update account setting](#update_account_setting)

## [DocuSign](#DocuSign)
* [Send DocuSign](#send docusign)
* [Check for DocuSign status](#check_docusign_status)

## [Feedback](#Feedback)
* [Send feedback](#send_feedback) 

## [payment statusnt](#Payment)
* [Get token](#get_token)
* [Check for payment status](#check_cc_status)
* [Handle payment method nonce](#add_nonce)
* [Get payment history](#get_payment_history)

## [Streaming](#Streaming)
* [Get streaming token](#get_streaming_token)
* [Stream has been started](#stream_started)
* [Stream has been received](#stream_received)
* [Stream finished](#stream_finished)

## [Rating](#Rating)
* [Rate stream](#rate_stream)



## <a name="Registration">Registration</a>
### <a name="new_account">Create new account </a>
```javascript
post /accounts
```
#### Body
```javascript
{
  "firstName": "hoa", //String, REQUIRED
  "lastName": "nguyen",  //String, REQUIRED
  "state":"CA",
  "country":"Vietnam",
  "city":"Saigon",
  "street":"Test street",
  "language":"VI",
  "archive":false, // [true, false]
  "status":"active", // ['active', 'banned'] 
  "type":"user",  // ['robot', 'trial', 'user', 'consumer', 'tester', 'customerSupport', 'admin']
  "identities": [ //There must be two elements, REQUIRED
    {
      "value": "12345678", //String, REQUIRED
      "type": "phone" //String, REQUIRED
    },
    {
      "value": "abcdefgh", //String, REQUIRED
      "type": "email" //String, REQUIRED
    }
  ]
}
```

#### Response
```javascript
{
    "token": {
        "account": "56011e197db2f56e35887d6f",
        "attempts": 0,
        "status": "unverified",
        "expiresOn": "2015-09-22T09:53:37.516Z",
        "code": "4478", //Save this field for latter verification
        "createdAt": "2015-09-22T09:23:37.517Z",
        "updatedAt": "2015-09-22T09:23:37.517Z",
        "id": "56011e197db2f56e35887d72", //Save this field for latter verification,
        "location": {
            "lat": 34.0851002, //Default latitude
            "lng": -118.3768646 //Default longitude
        }
    },
    "account": {
        "identities": [
            {
                "value": "12345678",
                "type": "phone",
                "status": "unverified",
                "createdAt": "2015-09-22T09:23:37.495Z",
                "updatedAt": "2015-09-22T09:23:37.495Z",
                "id": "56011e197db2f56e35887d70"
            },
            {
                "value": "abcdefgh",
                "type": "email",
                "status": "unverified",
                "createdAt": "2015-09-22T09:23:37.495Z",
                "updatedAt": "2015-09-22T09:23:37.495Z",
                "id": "56011e197db2f56e35887d71"
            }
        ],
        "firstName": "hoa",
        "lastName": "nguyen",
        "status": "active",
        "type": "user",
        "createdAt": "2015-09-22T09:23:37.486Z",
        "updatedAt": "2015-09-22T09:23:37.490Z",
        "id": "56011e197db2f56e35887d6f"
    }
}
```
## <a name="Authorization">Authorization</a>
### <a name='login'>Login</a>
```javascript
post /login
```
#### Body
```javascript
{
  "phone":"12345678", //String, REQUIRED
  "email":"abcdefgh" //String, REQUIRED
}
```
#### Response
```javascript
{
    "account": "56011e197db2f56e35887d6f",
    "attempts": 0,
    "status": "unverified",
    "expiresOn": "2015-09-22T09:57:01.191Z",
    "code": "0643", //Save this field for latter verification
    "createdAt": "2015-09-22T09:27:01.191Z",
    "updatedAt": "2015-09-22T09:27:01.191Z",
    "id": "56011ee57db2f56e35887d73", //Save this field for latter verification
     "location": {
            "lat": 34.0851002, //Default latitude
            "lng": -118.3768646 //Default longitude
        }
}
```
### <a name='verify'>Verify token</a>
```javascript
post /login/verify
```
#### Body
```javascript
{
  "tokenId":"56011ee57db2f56e35887d73", //String, REQUIRED
  "code":"0643"
}
```

#### Response
```javascript
{
    "token": "eyJ0eXAiOiJKV1QiLCJhbGciOiJIUzI1NiJ9.eyJhY2NvdW50SWQiOiI1NjAxMWUxOTdkYjJmNTZlMzU4ODdkNmYiLCJwZXJtaXNzaW9ucyI6W10sImlhdCI6MTQ0MjkxNDE0NiwiYXVkIjoiZHJvcGluLmNvbSIsImlzcyI6ImRyb3Bpbi5jb20ifQ.wt4P_elQAR8DIsLJPb8OENb8nfTb4aYdmEzu_3I8Hlk",
    //save this field for authorize API
    "account": {
        "identities": [
            {
                "value": "12345678",
                "type": "phone",
                "status": "unverified",
                "createdAt": "2015-09-22T09:23:37.495Z",
                "updatedAt": "2015-09-22T09:23:37.495Z",
                "id": "56011e197db2f56e35887d70"
            },
            {
                "value": "abcdefgh",
                "type": "email",
                "status": "unverified",
                "createdAt": "2015-09-22T09:23:37.495Z",
                "updatedAt": "2015-09-22T09:23:37.495Z",
                "id": "56011e197db2f56e35887d71"
            }
        ],
        "firstName": "hoa",
        "lastName": "nguyen",
        "status": "active",
        "type": "user",
        "createdAt": "2015-09-22T09:23:37.486Z",
        "updatedAt": "2015-09-22T09:23:37.490Z",
        "id": "56011e197db2f56e35887d6f"
    }
}
```
### <a name='logout'>Logout</a>
```javascript
post /logout
```
#### Body
```javascript
{
  "deviceAddress":"12345678" //String, REQUIRED
  
}
```
#### Response
```javascript
{
    "message":"ok"
}
```


## <a name="Device">Device</a>
### <a name='new_device'>Add new device to an account</a>
```javascript
post /devices/add
```
#### Headers
```javascript
{
"Content-Type":"application/json",
"Authorization":"Bearer eyJ0eXAiOiJKV1QiLCJhbGciOiJIUzI1NiJ9.eyJhY2NvdW50SWQiOiI1NjAxMWUxOTdkYjJmNTZlMzU4ODdkNmYiLCJwZXJtaXNzaW9ucyI6W10sImlhdCI6MTQ0MjkxNDE0NiwiYXVkIjoiZHJvcGluLmNvbSIsImlzcyI6ImRyb3Bpbi5jb20ifQ.wt4P_elQAR8DIsLJPb8OENb8nfTb4aYdmEzu_3I8Hlk"
}
```
#### Body
```javascript
 {
    "deviceAddress":"APA91bF4S5VIv9bg8katkkkh_4XJxI8j0efT5Dodgf95fVUSVsWbKZGyHgLwvOooJn1I", //String, REQUIRED
    "deviceType":"android" //String, REQUIRED ['android', 'ios']
 }
 ```


#### Response
```javascript
{
    "deviceAddress": "APA91bF4S5VIv9bg8katkkkh_4XJxI8j0efT5Dodgf95fVUSVsWbKZGyHgLwvOooJn1I-yjgbht91dM0yvSHqiY_l-a1No6gY9_2tQbUropwzrBfAcJCDgYlqQCxiSmEWJY8nataDmAy",
    "deviceType": "android",
    "account": "56011e197db2f56e35887d6f",
    "status": "active",
    "createdAt": "2015-09-22T09:30:31.767Z",
    "updatedAt": "2015-09-22T09:30:31.767Z",
    "id": "56011fb77db2f56e35887d74"
}
```
## <a name="Notification">Notification</a>

### <a name='send_notification'>Send notification (working on both android and ios)</a>
```javascript
post /notifications/send
```
#### Headers
```javascript
{
"Content-Type":"application/json",
"Authorization":"Bearer eyJ0eXAiOiJKV1QiLCJhbGciOiJIUzI1NiJ9.eyJhY2NvdW50SWQiOiI1NjAxMWUxOTdkYjJmNTZlMzU4ODdkNmYiLCJwZXJtaXNzaW9ucyI6W10sImlhdCI6MTQ0MjkxNDE0NiwiYXVkIjoiZHJvcGluLmNvbSIsImlzcyI6ImRyb3Bpbi5jb20ifQ.wt4P_elQAR8DIsLJPb8OENb8nfTb4aYdmEzu_3I8Hlk"
}
```
#### Body
```javascript
{
  "recipientId":"5560122297db2f56e35887d76", //id of account to send, String, REQUIRED
  "message":"Test" //messge to be sent, String, REQUIRED
}
```

#### Response
* OK: Status 200
* Failed: Status 400 or 500

### <a name='mark_notification_read'>Mark notification as read </a>
```javascript
patch notifications/:notificationId
```
#### Headers
```javascript
{
"Content-Type":"application/json",
"Authorization":"Bearer eyJ0eXAiOiJKV1QiLCJhbGciOiJIUzI1NiJ9.eyJhY2NvdW50SWQiOiI1NjAxMWUxOTdkYjJmNTZlMzU4ODdkNmYiLCJwZXJtaXNzaW9ucyI6W10sImlhdCI6MTQ0MjkxNDE0NiwiYXVkIjoiZHJvcGluLmNvbSIsImlzcyI6ImRyb3Bpbi5jb20ifQ.wt4P_elQAR8DIsLJPb8OENb8nfTb4aYdmEzu_3I8Hlk"
}
```
#### Body
```javascript
{
  "status":"received",
  "id":SHOUD BE THE SAME TO NOTIFICATIONID //id of notification to mark, String, REQUIRED
 }
```

#### Response
```javascript
[
    {
        "sender": "560cf0e4e33524f016a8d60c",
        "recipient": "560cf0e4e33524f016a8d60c",
        "message": "test",
        "status": "received",
        "archive": false,
        "type": "real",
        "createdAt": "2015-10-01T18:10:57.774Z",
        "updatedAt": "2015-10-01T18:25:44.451Z",
        "id": "560d78728bfcc5a2c8eec708"
    }
]
```
### <a name='get_unread_list_notification'>Get list of unread notification </a>
```javascript
get /notifications/unread
```
#### Headers
```javascript
{
"Content-Type":"application/json",
"Authorization":"Bearer eyJ0eXAiOiJKV1QiLCJhbGciOiJIUzI1NiJ9.eyJhY2NvdW50SWQiOiI1NjAxMWUxOTdkYjJmNTZlMzU4ODdkNmYiLCJwZXJtaXNzaW9ucyI6W10sImlhdCI6MTQ0MjkxNDE0NiwiYXVkIjoiZHJvcGluLmNvbSIsImlzcyI6ImRyb3Bpbi5jb20ifQ.wt4P_elQAR8DIsLJPb8OENb8nfTb4aYdmEzu_3I8Hlk"
}
```

#### Response
```javascript
{
    "messages": [
        {
            "sender": {
                "firstName": "Dropin",
                "lastName": "",
                "city": "LA",
                "country": "USA",
                "languate": "English",
                "state": "CA",
                "street": "Diamond"
            },
            "recipient": "561238b17c2261981a565379",
            "message": "You have successfully signed in from new device",
            "status": "sent", //['pending', 'sent', 'failed', 'received'], pending: sending, sent: sent, failed: failed to send, received: sent and read
            "code": 0,
            "title": "A message from Droppin",
            "archive": false,
            "type": "real",
            "createdAt": "2015-10-05T08:37:15.821Z",
            "updatedAt": "2015-10-05T08:37:15.821Z",
            "id": "561378fef9932ddf5941ad5f"
        },
        {
            "sender": {
                "firstName": "Dropin",
                "lastName": "",
                "city": "LA",
                "country": "USA",
                "languate": "English",
                "state": "CA",
                "street": "Diamond"
            },
            "recipient": "561238b17c2261981a565379",
            "message": "You have successfully signed in from new device",
            "status": "sent",
            "code": 0,
            "title": "A message from Droppin",
            "archive": false,
            "type": "real",
            "createdAt": "2015-10-05T08:37:15.821Z",
            "updatedAt": "2015-10-05T08:37:15.821Z",
            "id": "561236bbe792a3ec137b34e7"
        }
    ]
}
```

### <a name='get_list_notification'>Get list of notification </a>
```javascript
get /notifications?status=sent
```
#### Headers
```javascript
{
"Content-Type":"application/json",
"Authorization":"Bearer eyJ0eXAiOiJKV1QiLCJhbGciOiJIUzI1NiJ9.eyJhY2NvdW50SWQiOiI1NjAxMWUxOTdkYjJmNTZlMzU4ODdkNmYiLCJwZXJtaXNzaW9ucyI6W10sImlhdCI6MTQ0MjkxNDE0NiwiYXVkIjoiZHJvcGluLmNvbSIsImlzcyI6ImRyb3Bpbi5jb20ifQ.wt4P_elQAR8DIsLJPb8OENb8nfTb4aYdmEzu_3I8Hlk"
}
```

#### Response
```javascript
{
    "messages": [
        {
            "sender": {
                "firstName": "Dropin",
                "lastName": "",
                "city": "LA",
                "country": "USA",
                "languate": "English",
                "state": "CA",
                "street": "Diamond"
            },
            "recipient": "561238b17c2261981a565379",
            "message": "You have successfully signed in from new device",
            "status": "sent", //['pending', 'sent', 'failed', 'received'], pending: sending, sent: sent, failed: failed to send, received: sent and read
            "code": 0,
            "title": "A message from Droppin",
            "archive": false,
            "type": "real",
            "createdAt": "2015-10-05T08:37:15.821Z",
            "updatedAt": "2015-10-05T08:37:15.821Z",
            "id": "561378fef9932ddf5941ad5f"
        },
        {
            "sender": {
                "firstName": "Dropin",
                "lastName": "",
                "city": "LA",
                "country": "USA",
                "languate": "English",
                "state": "CA",
                "street": "Diamond"
            },
            "recipient": "561238b17c2261981a565379",
            "message": "You have successfully signed in from new device",
            "status": "sent",
            "code": 0,
            "title": "A message from Droppin",
            "archive": false,
            "type": "real",
            "createdAt": "2015-10-05T08:37:15.821Z",
            "updatedAt": "2015-10-05T08:37:15.821Z",
            "id": "561236bbe792a3ec137b34e7"
        }
    ]
}
```

### <a name='get_notification'>Get notification </a>
```javascript
get /notifications/get
```
#### Headers
```javascript
{
"Content-Type":"application/json",
"Authorization":"Bearer eyJ0eXAiOiJKV1QiLCJhbGciOiJIUzI1NiJ9.eyJhY2NvdW50SWQiOiI1NjAxMWUxOTdkYjJmNTZlMzU4ODdkNmYiLCJwZXJtaXNzaW9ucyI6W10sImlhdCI6MTQ0MjkxNDE0NiwiYXVkIjoiZHJvcGluLmNvbSIsImlzcyI6ImRyb3Bpbi5jb20ifQ.wt4P_elQAR8DIsLJPb8OENb8nfTb4aYdmEzu_3I8Hlk"
}
```
#### Query
```javascript
{
"notificationId": '3243242432432432432432' //String, required
"update": 'true' //String, optional, the notification will automatically be marked as read if update=true
```

#### Response
```javascript
{
    "sender": {
        "firstName": "Dropin",
        "lastName": "",
        "city": "LA",
        "country": "USA",
        "languate": "English",
        "state": "CA",
        "street": "Diamond"
    },
    "recipient": "561238b17c2261981a565379",
    "message": "You have successfully signed in from new device",
    "status": "received", //['pending', 'sent', 'failed', 'received'], pending: sending, sent: sent, failed: failed to send, received: sent and read
    "code": 0,
    "title": "A message from Droppin",
    "archive": false,
    "type": "real",
    "createdAt": "2015-10-05T08:37:15.821Z",
    "updatedAt": "2015-10-05T08:37:15.821Z",
    "id": "561378d3f9932ddf5941ad5e"
}
```
### <a name='remove_notification'>Remove notification </a>
```javascript
delete /notifications
```
#### Headers
```javascript
{
"Content-Type":"application/json",
"Authorization":"Bearer eyJ0eXAiOiJKV1QiLCJhbGciOiJIUzI1NiJ9.eyJhY2NvdW50SWQiOiI1NjAxMWUxOTdkYjJmNTZlMzU4ODdkNmYiLCJwZXJtaXNzaW9ucyI6W10sImlhdCI6MTQ0MjkxNDE0NiwiYXVkIjoiZHJvcGluLmNvbSIsImlzcyI6ImRyb3Bpbi5jb20ifQ.wt4P_elQAR8DIsLJPb8OENb8nfTb4aYdmEzu_3I8Hlk"
}
```
#### Body
```javascript
{
  "notificationId":"5560122297db2f56e35887d76" //id of notification to delete, String, REQUIRED
 }
```

#### Response
```javascript
[
    {
        "sender": "560cf0e4e33524f016a8d60c",
        "recipient": "560cf0e4e33524f016a8d60c",
        "message": "test",
        "status": "pending",
        "archive": false,
        "type": "real",
        "createdAt": "2015-10-01T18:10:57.774Z",
        "updatedAt": "2015-10-01T18:10:57.774Z",
        "id": "560d7bcc8bfcc5a2c8eec70a"
    }
]
```


## <a name="Profile">Profile</a>

### Note: Body *id* must match with params *id*

### <a name='update_account_profile'>Update account</a>
```javascript
Put /accounts/:accountId
```
#### Headers
```javascript
{
"Content-Type":"application/json",
"Authorization":"Bearer eyJ0eXAiOiJKV1QiLCJhbGciOiJIUzI1NiJ9.eyJhY2NvdW50SWQiOiI1NjAxMWUxOTdkYjJmNTZlMzU4ODdkNmYiLCJwZXJtaXNzaW9ucyI6W10sImlhdCI6MTQ0MjkxNDE0NiwiYXVkIjoiZHJvcGluLmNvbSIsImlzcyI6ImRyb3Bpbi5jb20ifQ.wt4P_elQAR8DIsLJPb8OENb8nfTb4aYdmEzu_3I8Hlk"
}
```

#### Body
```javascript
{
  "id":"4535435gsgfewg54"
  "firstName": "hoa", //String, REQUIRED
  "lastName": "nguyen",  //String, REQUIRED
  "state":"CA",
  "country":"Vietnam",
  "city":"Saigon",
  "street":"Test street",
  "language":"VI"
}
```
#### Params
```javascript
{
  "accountId":"4535435gsgfewg54"
 }
```
#### Response
```javascript
{
   "identities": [
            {
              
                "id": "56011e197db2f56e35887d70"
            },
            {
              
                "id": "56011e197db2f56e35887d71"
            }
        ],
        "firstName": "hoa",
        "lastName": "nguyen",
        "status": "active",
        "type": "user",
        "createdAt": "2015-09-22T09:23:37.486Z",
        "updatedAt": "2015-09-22T09:23:37.490Z",
        "id": "56011e197db2f56e35887d6f"
}
```

### <a name='get_account_profile'>Get account profile</a>
```javascript
get /accounts/:accountId
```

#### Headers
```javascript
{
"Content-Type":"application/json",
"Authorization":"Bearer eyJ0eXAiOiJKV1QiLCJhbGciOiJIUzI1NiJ9.eyJhY2NvdW50SWQiOiI1NjAxMWUxOTdkYjJmNTZlMzU4ODdkNmYiLCJwZXJtaXNzaW9ucyI6W10sImlhdCI6MTQ0MjkxNDE0NiwiYXVkIjoiZHJvcGluLmNvbSIsImlzcyI6ImRyb3Bpbi5jb20ifQ.wt4P_elQAR8DIsLJPb8OENb8nfTb4aYdmEzu_3I8Hlk"
}
```

#### Response
```javascript
{
    "identities": [
        {
            "value": "123",
            "type": "phone",
            "account": "5608c5588a4e36915d59c9d2",
            "archive": false,
            "status": "unverified",
            "createdAt": "2015-09-28T04:43:04.822Z",
            "updatedAt": "2015-09-28T04:43:04.822Z",
            "id": "5608c5588a4e36915d59c9d3"
        },
        {
            "value": "abc",
            "type": "email",
            "account": "5608c5588a4e36915d59c9d2",
            "archive": false,
            "status": "unverified",
            "createdAt": "2015-09-28T04:43:04.826Z",
            "updatedAt": "2015-09-28T04:43:04.826Z",
            "id": "5608c5588a4e36915d59c9d4"
        }
    ],
    "firstName": "hoa",
    "lastName": "nguyen",
    "archive": false,
    "status": "active",
    "type": "user",
    "createdAt": "2015-09-28T04:43:04.773Z",
    "updatedAt": "2015-09-28T04:43:04.804Z",
    "id": "5608c5588a4e36915d59c9d2"
}
```
### <a name='deactivate_account'>Deactivate account</a>
```javascript
delete /accounts/:accountId
```

#### Headers
```javascript
{
"Content-Type":"application/json",
"Authorization":"Bearer eyJ0eXAiOiJKV1QiLCJhbGciOiJIUzI1NiJ9.eyJhY2NvdW50SWQiOiI1NjAxMWUxOTdkYjJmNTZlMzU4ODdkNmYiLCJwZXJtaXNzaW9ucyI6W10sImlhdCI6MTQ0MjkxNDE0NiwiYXVkIjoiZHJvcGluLmNvbSIsImlzcyI6ImRyb3Bpbi5jb20ifQ.wt4P_elQAR8DIsLJPb8OENb8nfTb4aYdmEzu_3I8Hlk"
}
```

#### Response
```javascript
Status 200: Success
Status !=200: Failed
```


## <a name="Setting">Setting</a>

### <a name='get_account_setting'>Get account setting</a>
```javascript
get /accountsetting
```
#### Headers
```javascript
{
"Content-Type":"application/json",
"Authorization":"Bearer eyJ0eXAiOiJKV1QiLCJhbGciOiJIUzI1NiJ9.eyJhY2NvdW50SWQiOiI1NjAxMWUxOTdkYjJmNTZlMzU4ODdkNmYiLCJwZXJtaXNzaW9ucyI6W10sImlhdCI6MTQ0MjkxNDE0NiwiYXVkIjoiZHJvcGluLmNvbSIsImlzcyI6ImRyb3Bpbi5jb20ifQ.wt4P_elQAR8DIsLJPb8OENb8nfTb4aYdmEzu_3I8Hlk"
}
```

#### Response
```javascript
{
    "account": "560d0eb9ff4f0358a035d6a7",
    "detectRadius": 1000,
    "defaultLatitude": 34.0851002,
    "defaultLongitude": -118.3768646,
    "createdAt": "2015-10-01T19:24:56.305Z",
    "updatedAt": "2015-10-01T19:24:56.305Z",
    "id": "560d88881b2627e2f06e80e3"
}
```

### <a name='update_account_setting'>Update account setting</a>
```javascript
post /accountsetting
```

#### Headers
```javascript
{
"Content-Type":"application/json",
"Authorization":"Bearer eyJ0eXAiOiJKV1QiLCJhbGciOiJIUzI1NiJ9.eyJhY2NvdW50SWQiOiI1NjAxMWUxOTdkYjJmNTZlMzU4ODdkNmYiLCJwZXJtaXNzaW9ucyI6W10sImlhdCI6MTQ0MjkxNDE0NiwiYXVkIjoiZHJvcGluLmNvbSIsImlzcyI6ImRyb3Bpbi5jb20ifQ.wt4P_elQAR8DIsLJPb8OENb8nfTb4aYdmEzu_3I8Hlk"
}
```
#### Body
```javascript
{
  "detectRadius":40000,
  "defaultLatitude":12.23,
  "defaultLongitude":12.24
}
```
#### Response
```javascript
[{
    "account": "560d0eb9ff4f0358a035d6a7",
    "detectRadius": 1000,
    "defaultLatitude": 34.0851002,
    "defaultLongitude": -118.3768646,
    "numberOfNotificationPerPage": 20
    "createdAt": "2015-10-01T19:24:56.305Z",
    "updatedAt": "2015-10-01T19:24:56.305Z",
    "id": "560d88881b2627e2f06e80e3"
}]
```


## <a name="DocuSign">DocuSign</a>

### <a name='send docusign'>Send DocuSign</a>
```javascript
post /docusign/send
```
#### Headers
```javascript
{
"Content-Type":"application/json",
"Authorization":"Bearer eyJ0eXAiOiJKV1QiLCJhbGciOiJIUzI1NiJ9.eyJhY2NvdW50SWQiOiI1NjAxMWUxOTdkYjJmNTZlMzU4ODdkNmYiLCJwZXJtaXNzaW9ucyI6W10sImlhdCI6MTQ0MjkxNDE0NiwiYXVkIjoiZHJvcGluLmNvbSIsImlzcyI6ImRyb3Bpbi5jb20ifQ.wt4P_elQAR8DIsLJPb8OENb8nfTb4aYdmEzu_3I8Hlk"
}
```

#### Response
```javascript

    {
        "account": "561238b17c2261981a565379",
        "taxFormId": "1234",
        "vendorId": "1234",
        "status": "pending",
        "createdAt": "2015-10-05T10:28:57.092Z",
        "updatedAt": "2015-10-05T10:29:09.637Z",
        "id": "561250e9fce552d41926becb"
    }

```
### <a name='check_docusign_status'>Check for docusign status of account</a>
```javascript
get /docusign/status
```
#### Headers
```javascript
{
"Content-Type":"application/json",
"Authorization":"Bearer eyJ0eXAiOiJKV1QiLCJhbGciOiJIUzI1NiJ9.eyJhY2NvdW50SWQiOiI1NjAxMWUxOTdkYjJmNTZlMzU4ODdkNmYiLCJwZXJtaXNzaW9ucyI6W10sImlhdCI6MTQ0MjkxNDE0NiwiYXVkIjoiZHJvcGluLmNvbSIsImlzcyI6ImRyb3Bpbi5jb20ifQ.wt4P_elQAR8DIsLJPb8OENb8nfTb4aYdmEzu_3I8Hlk"
}
```

#### Response
```javascript
{
    "status": "completed",
    "documentsUri": "/envelopes/f8db85dc-e7d6-4030-835d-f00eea6aac09/documents",
    "recipientsUri": "/envelopes/f8db85dc-e7d6-4030-835d-f00eea6aac09/recipients",
    "envelopeUri": "/envelopes/f8db85dc-e7d6-4030-835d-f00eea6aac09",
    "emailSubject": "[Action required - Dropin]",
    "envelopeId": "f8db85dc-e7d6-4030-835d-f00eea6aac09",
    "customFieldsUri": "/envelopes/f8db85dc-e7d6-4030-835d-f00eea6aac09/custom_fields",
    "notificationUri": "/envelopes/f8db85dc-e7d6-4030-835d-f00eea6aac09/notification",
    "enableWetSign": "true",
    "allowMarkup": "false",
    "allowReassign": "true",
    "createdDateTime": "2015-10-05T10:37:43.3100000Z",
    "lastModifiedDateTime": "2015-10-05T10:37:43.3100000Z",
    "deliveredDateTime": "2015-10-05T10:38:28.3030000Z",
    "sentDateTime": "2015-10-05T10:37:44.2800000Z",
    "completedDateTime": "2015-10-05T10:38:39.6600000Z",
    "statusChangedDateTime": "2015-10-05T10:38:39.6600000Z",
    "documentsCombinedUri": "/envelopes/f8db85dc-e7d6-4030-835d-f00eea6aac09/documents/combined",
    "certificateUri": "/envelopes/f8db85dc-e7d6-4030-835d-f00eea6aac09/documents/certificate",
    "templatesUri": "/envelopes/f8db85dc-e7d6-4030-835d-f00eea6aac09/templates",
    "purgeState": "unpurged"
}
```


## <a name="Feedback">Feedback</a>

### <a name='send_feedback'>Send feedback</a>
```javascript
post /sendfeedback
```
#### Headers
```javascript
{
"Content-Type":"application/json",
"Authorization":"Bearer eyJ0eXAiOiJKV1QiLCJhbGciOiJIUzI1NiJ9.eyJhY2NvdW50SWQiOiI1NjAxMWUxOTdkYjJmNTZlMzU4ODdkNmYiLCJwZXJtaXNzaW9ucyI6W10sImlhdCI6MTQ0MjkxNDE0NiwiYXVkIjoiZHJvcGluLmNvbSIsImlzcyI6ImRyb3Bpbi5jb20ifQ.wt4P_elQAR8DIsLJPb8OENb8nfTb4aYdmEzu_3I8Hlk"
}
```

#### Body

```javascript
{
  "title":"Test",
  "content":"This is feedbacfdsgfdsgfdsgfdsgfdhgfdhgfdhgfdhhgfdhgfddsgk"
}
    
```

#### Response
```javascript
{
    "account": "561238b17c2261981a565379",
    "title": "Test",
    "content": "This is feedbacfdsgfdsgfdsgfdsgfdhgfdhgfdhgfdhhgfdhgfddsgk",
    "tags": [
        "feedback"
    ],
    "archive": false,
    "type": "real",
    "createdAt": "2015-10-06T10:30:44.418Z",
    "updatedAt": "2015-10-06T10:30:44.418Z",
    "id": "5613a2d4ca0dc4e4160fe438"
}
```


## <a name="Payment">Payment</a>

### <a name='check_cc_status'>Check for payment status</a>
```javascript
get /purchases/paymentMethods
```
#### Headers
```javascript
{
"Content-Type":"application/json",
"Authorization":"Bearer eyJ0eXAiOiJKV1QiLCJhbGciOiJIUzI1NiJ9.eyJhY2NvdW50SWQiOiI1NjAxMWUxOTdkYjJmNTZlMzU4ODdkNmYiLCJwZXJtaXNzaW9ucyI6W10sImlhdCI6MTQ0MjkxNDE0NiwiYXVkIjoiZHJvcGluLmNvbSIsImlzcyI6ImRyb3Bpbi5jb20ifQ.wt4P_elQAR8DIsLJPb8OENb8nfTb4aYdmEzu_3I8Hlk"
}
```


#### Response
```javascript
{
   
    "code": 'CARD_OK', //['CARD_OK', 'ALL_CARDS_EXPIRED', 'NO_CARD'] 0: expired, 1: no cc, 2 :ok
     "payments": [
        {
            "billingAddress": {
                "id": "6y",
                "customerId": "561e26b0120620d003e8ca5d",
                "firstName": null,
                "lastName": null,
                "company": null,
                "streetAddress": null,
                "extendedAddress": null,
                "locality": null,
                "region": null,
                "postalCode": "94107",
                "countryCodeAlpha2": null,
                "countryCodeAlpha3": null,
                "countryCodeNumeric": null,
                "countryName": null,
                "createdAt": "2015-10-15T03:54:04Z",
                "updatedAt": "2015-10-15T03:54:04Z"
            },
            "bin": "401288",
            "cardType": "Visa",
            "cardholderName": null,
            "commercial": "Unknown",
            "countryOfIssuance": "USA",
            "createdAt": "2015-10-15T03:54:04Z",
            "customerId": "561e26b0120620d003e8ca5d",
            "customerLocation": "US",
            "debit": "Unknown",
            "default": true,
            "durbinRegulated": "Unknown",
            "expirationMonth": "12",
            "expirationYear": "2020",
            "expired": false,
            "healthcare": "Unknown",
            "imageUrl": "https://assets.braintreegateway.com/payment_method_logo/visa.png?environment=sandbox",
            "issuingBank": "Unknown",
            "last4": "1881",
            "payroll": "Unknown",
            "prepaid": "No",
            "subscriptions": [],
            "token": "jfzmdg",
            "uniqueNumberIdentifier": "60264ac57bc9b29b428f4724c45eb690",
            "updatedAt": "2015-10-15T03:54:04Z",
            "venmoSdk": false,
            "verifications": [
                {
                    "status": "verified",
                    "cvvResponseCode": "M",
                    "avsErrorResponseCode": null,
                    "avsPostalCodeResponseCode": "M",
                    "avsStreetAddressResponseCode": "I",
                    "gatewayRejectionReason": null,
                    "merchantAccountId": "dropin",
                    "processorResponseCode": "1000",
                    "processorResponseText": "Approved",
                    "id": "63fyq4",
                    "billing": {
                        "firstName": null,
                        "lastName": null,
                        "company": null,
                        "streetAddress": null,
                        "extendedAddress": null,
                        "locality": null,
                        "region": null,
                        "postalCode": "94107",
                        "countryName": null
                    },
                    "creditCard": {
                        "token": "jfzmdg",
                        "bin": "401288",
                        "last4": "1881",
                        "cardType": "Visa",
                        "expirationMonth": "12",
                        "expirationYear": "2020",
                        "customerLocation": "US",
                        "cardholderName": null,
                        "uniqueNumberIdentifier": "60264ac57bc9b29b428f4724c45eb690",
                        "prepaid": "No",
                        "healthcare": "Unknown",
                        "debit": "Unknown",
                        "durbinRegulated": "Unknown",
                        "commercial": "Unknown",
                        "payroll": "Unknown",
                        "issuingBank": "Unknown",
                        "countryOfIssuance": "USA",
                        "productId": "Unknown"
                    },
                    "createdAt": "2015-10-15T03:54:04Z",
                    "updatedAt": "2015-10-15T03:54:04Z"
                }
            ],
            "maskedNumber": "401288******1881",
            "expirationDate": "12/2020",
            "verification": {
                "status": "verified",
                "cvvResponseCode": "M",
                "avsErrorResponseCode": null,
                "avsPostalCodeResponseCode": "M",
                "avsStreetAddressResponseCode": "I",
                "gatewayRejectionReason": null,
                "merchantAccountId": "dropin",
                "processorResponseCode": "1000",
                "processorResponseText": "Approved",
                "id": "63fyq4",
                "billing": {
                    "firstName": null,
                    "lastName": null,
                    "company": null,
                    "streetAddress": null,
                    "extendedAddress": null,
                    "locality": null,
                    "region": null,
                    "postalCode": "94107",
                    "countryName": null
                },
                "creditCard": {
                    "token": "jfzmdg",
                    "bin": "401288",
                    "last4": "1881",
                    "cardType": "Visa",
                    "expirationMonth": "12",
                    "expirationYear": "2020",
                    "customerLocation": "US",
                    "cardholderName": null,
                    "uniqueNumberIdentifier": "60264ac57bc9b29b428f4724c45eb690",
                    "prepaid": "No",
                    "healthcare": "Unknown",
                    "debit": "Unknown",
                    "durbinRegulated": "Unknown",
                    "commercial": "Unknown",
                    "payroll": "Unknown",
                    "issuingBank": "Unknown",
                    "countryOfIssuance": "USA",
                    "productId": "Unknown"
                },
                "createdAt": "2015-10-15T03:54:04Z",
                "updatedAt": "2015-10-15T03:54:04Z"
            }
        }
    ]
}
```
## <a name='get_token'>Get token</a>
```javascript
get /payment/token
```
#### Headers
```javascript
{
"Content-Type":"application/json",
"Authorization":"Bearer eyJ0eXAiOiJKV1QiLCJhbGciOiJIUzI1NiJ9.eyJhY2NvdW50SWQiOiI1NjAxMWUxOTdkYjJmNTZlMzU4ODdkNmYiLCJwZXJtaXNzaW9ucyI6W10sImlhdCI6MTQ0MjkxNDE0NiwiYXVkIjoiZHJvcGluLmNvbSIsImlzcyI6ImRyb3Bpbi5jb20ifQ.wt4P_elQAR8DIsLJPb8OENb8nfTb4aYdmEzu_3I8Hlk"
}
```


#### Response
```javascript
{

    "clientToken": "eyJ2ZXJzaW9uIjoyLCJhdXRob3JpemF0aW9uRmluZ2VycHJpbnQiOiIzY2YzYmNjMDA2MGI0YTAxMGQyMDdhNWE1YzI3MzdjMWMxNGYxZjU4MmEzZDIxYmViN2E2ZTJjZmY5MTExNDI4fGNyZWF0ZWRfYXQ9MjAxNS0xMC0wOFQwOToxODozNi40MjcwMDIyMzcrMDAwMFx1MDAyNm1lcmNoYW50X2lkPTV6NGpmZjVmM2o0Z2J0djNcdTAwMjZwdWJsaWNfa2V5PXlzZjJtcjd3c2s2NXc1Z3QiLCJjb25maWdVcmwiOiJodHRwczovL2FwaS5zYW5kYm94LmJyYWludHJlZWdhdGV3YXkuY29tOjQ0My9tZXJjaGFudHMvNXo0amZmNWYzajRnYnR2My9jbGllbnRfYXBpL3YxL2NvbmZpZ3VyYXRpb24iLCJjaGFsbGVuZ2VzIjpbXSwiZW52aXJvbm1lbnQiOiJzYW5kYm94IiwiY2xpZW50QXBpVXJsIjoiaHR0cHM6Ly9hcGkuc2FuZGJveC5icmFpbnRyZWVnYXRld2F5LmNvbTo0NDMvbWVyY2hhbnRzLzV6NGpmZjVmM2o0Z2J0djMvY2xpZW50X2FwaSIsImFzc2V0c1VybCI6Imh0dHBzOi8vYXNzZXRzLmJyYWludHJlZWdhdGV3YXkuY29tIiwiYXV0aFVybCI6Imh0dHBzOi8vYXV0aC52ZW5tby5zYW5kYm94LmJyYWludHJlZWdhdGV3YXkuY29tIiwiYW5hbHl0aWNzIjp7InVybCI6Imh0dHBzOi8vY2xpZW50LWFuYWx5dGljcy5zYW5kYm94LmJyYWludHJlZWdhdGV3YXkuY29tIn0sInRocmVlRFNlY3VyZUVuYWJsZWQiOmZhbHNlLCJwYXlwYWxFbmFibGVkIjp0cnVlLCJwYXlwYWwiOnsiZGlzcGxheU5hbWUiOiJEcm9wIEluIiwiY2xpZW50SWQiOm51bGwsInByaXZhY3lVcmwiOiJodHRwOi8vZXhhbXBsZS5jb20vcHAiLCJ1c2VyQWdyZWVtZW50VXJsIjoiaHR0cDovL2V4YW1wbGUuY29tL3RvcyIsImJhc2VVcmwiOiJodHRwczovL2Fzc2V0cy5icmFpbnRyZWVnYXRld2F5LmNvbSIsImFzc2V0c1VybCI6Imh0dHBzOi8vY2hlY2tvdXQucGF5cGFsLmNvbSIsImRpcmVjdEJhc2VVcmwiOm51bGwsImFsbG93SHR0cCI6dHJ1ZSwiZW52aXJvbm1lbnROb05ldHdvcmsiOnRydWUsImVudmlyb25tZW50Ijoib2ZmbGluZSIsInVudmV0dGVkTWVyY2hhbnQiOmZhbHNlLCJicmFpbnRyZWVDbGllbnRJZCI6Im1hc3RlcmNsaWVudDMiLCJiaWxsaW5nQWdyZWVtZW50c0VuYWJsZWQiOm51bGwsIm1lcmNoYW50QWNjb3VudElkIjoiZHJvcGluIiwiY3VycmVuY3lJc29Db2RlIjoiVVNEIn0sImNvaW5iYXNlRW5hYmxlZCI6ZmFsc2UsIm1lcmNoYW50SWQiOiI1ejRqZmY1ZjNqNGdidHYzIiwidmVubW8iOiJvZmYifQ==",
    "success": true

}
```
## <a name='add_nonce'>Add credit card nonce</a>
```javascript
post /payment/handlePaymentMethodNonce
```
#### Headers
```javascript
{
"Content-Type":"application/json",
"Authorization":"Bearer eyJ0eXAiOiJKV1QiLCJhbGciOiJIUzI1NiJ9.eyJhY2NvdW50SWQiOiI1NjAxMWUxOTdkYjJmNTZlMzU4ODdkNmYiLCJwZXJtaXNzaW9ucyI6W10sImlhdCI6MTQ0MjkxNDE0NiwiYXVkIjoiZHJvcGluLmNvbSIsImlzcyI6ImRyb3Bpbi5jb20ifQ.wt4P_elQAR8DIsLJPb8OENb8nfTb4aYdmEzu_3I8Hlk"
}
```


#### Body

```javascript
{
  "nonce":"1312321"
}
    
```

#### Response
```javascript
{
    "message": 'ok'
}
```

## <a name='get_payment_history'>Get payment history</a>
```javascript
get /payment/history
```
#### Headers
```javascript
{
"Content-Type":"application/json",
"Authorization":"Bearer eyJ0eXAiOiJKV1QiLCJhbGciOiJIUzI1NiJ9.eyJhY2NvdW50SWQiOiI1NjAxMWUxOTdkYjJmNTZlMzU4ODdkNmYiLCJwZXJtaXNzaW9ucyI6W10sImlhdCI6MTQ0MjkxNDE0NiwiYXVkIjoiZHJvcGluLmNvbSIsImlzcyI6ImRyb3Bpbi5jb20ifQ.wt4P_elQAR8DIsLJPb8OENb8nfTb4aYdmEzu_3I8Hlk"
}
```


#### Response
```javascript
{
    "payments": [
        {
            "firstName": "test",
            "lastName": "test",
            "date": "2015-10-08T10:28:02.156Z",
            "cost": 100,
            "rating": 4,
            "transactionType":"viewer/operator"
        },
        {
            "firstName": "test",
            "lastName": "test",
            "date": "2015-10-08T10:28:02.156Z",
            "cost": 100,
            "rating": 5,
             "transactionType":"viewer/operator"
        },
        {
            "firstName": "test",
            "lastName": "test",
            "date": "2015-10-08T10:28:02.157Z",
            "cost": 100,
            "rating": 4,
             "transactionType":"viewer/operator"
        },
        {
            "firstName": "test",
            "lastName": "test",
            "date": "2015-10-08T10:28:02.157Z",
            "cost": 100,
            "rating": 5,
             "transactionType":"viewer/operator"
        },
        {
            "firstName": "test",
            "lastName": "test",
            "date": "2015-10-08T10:28:02.157Z",
            "cost": 100,
            "rating": 1,
             "transactionType":"viewer/operator"
        },
        {
            "firstName": "test",
            "lastName": "test",
            "date": "2015-10-08T10:28:02.157Z",
            "cost": 100,
            "rating": 2,
             "transactionType":"viewer/operator"
        },
        {
            "firstName": "test",
            "lastName": "test",
            "date": "2015-10-08T10:28:02.157Z",
            "cost": 100,
            "rating": 3,
             "transactionType":"viewer/operator"
        },
        {
            "firstName": "test",
            "lastName": "test",
            "date": "2015-10-08T10:28:02.157Z",
            "cost": 100,
            "rating": 4,
             "transactionType":"viewer/operator"
        },
        {
            "firstName": "test",
            "lastName": "test",
            "date": "2015-10-08T10:28:02.157Z",
            "cost": 100,
            "rating": 3,
             "transactionType":"viewer/operator"
        },
        {
            "firstName": "test",
            "lastName": "test",
            "date": "2015-10-08T10:28:02.157Z",
            "cost": 100,
            "rating": 1,
             "transactionType":"viewer/operator"
        }
    ]
}
```


## <a name="Streaming">Streaming</a>
## <a name='get_streaming_token'>Get streaming token</a>
```javascript
post /streams/gettoken
```
#### Headers
```javascript
{
"Content-Type":"application/json",
"Authorization":"Bearer eyJ0eXAiOiJKV1QiLCJhbGciOiJIUzI1NiJ9.eyJhY2NvdW50SWQiOiI1NjAxMWUxOTdkYjJmNTZlMzU4ODdkNmYiLCJwZXJtaXNzaW9ucyI6W10sImlhdCI6MTQ0MjkxNDE0NiwiYXVkIjoiZHJvcGluLmNvbSIsImlzcyI6ImRyb3Bpbi5jb20ifQ.wt4P_elQAR8DIsLJPb8OENb8nfTb4aYdmEzu_3I8Hlk"
}
```
#### Body
```javascript
{
  "userId":"56188896f534e3781aa5798d",
  "operatorId":"56188896f534e3781aa5798d"
}
```


#### Response
```javascript
{
    "token": "T1==cGFydG5lcl9pZD00NTMzMTY0MiZzaWc9NGM5YjdlN2VhMDI0NjAwMjE1NGE4MmU3YzdlNWIwNDg2ZDhmODY5MjpzZXNzaW9uX2lkPTJfTVg0ME5UTXpNVFkwTW41LU1UUTBORFExTWprek5EZzNNSDR4VlRsT1ZYb3JXbk5rZG5sdWRXODVXSFpGYW5CbGRVaC1mZyZjcmVhdGVfdGltZT0xNDQ0NDUyOTM0Jm5vbmNlPTAuMTI1NDY3NDExMDA5NTk0OCZyb2xlPXB1Ymxpc2hlciZleHBpcmVfdGltZT0xNDQ1MDU3NzM0JmNvbm5lY3Rpb25fZGF0YT11c2VySWQlM0Q1NjE4ODg5NmY1MzRlMzc4MWFhNTc5OGQlM0JvcGVyYXRvcklkJTNENTYxODg4OTZmNTM0ZTM3ODFhYTU3OThk",
    "apiKey": "45331642",
    "sessionId": "2_MX40NTMzMTY0Mn5-MTQ0NDQ1MjkzNDg3MH4xVTlOVXorWnNkdnludW85WHZFanBldUh-fg"
}
```
## <a name='stream_started'>Stream started</a>

post /streams/streamstarted

```
#### Headers
```javascript
{
"Content-Type":"application/json",
"Authorization":"Bearer eyJ0eXAiOiJKV1QiLCJhbGciOiJIUzI1NiJ9.eyJhY2NvdW50SWQiOiI1NjAxMWUxOTdkYjJmNTZlMzU4ODdkNmYiLCJwZXJtaXNzaW9ucyI6W10sImlhdCI6MTQ0MjkxNDE0NiwiYXVkIjoiZHJvcGluLmNvbSIsImlzcyI6ImRyb3Bpbi5jb20ifQ.wt4P_elQAR8DIsLJPb8OENb8nfTb4aYdmEzu_3I8Hlk"
}
```
#### Body
```javascript
{
  "userId":"56188896f534e3781aa5798d",
  "operatorId":"56188896f534e3781aa5798d",
  "token":"T1==cGFydG5lcl9pZD00NTMzMTY0MiZzaWc9NGM5YjdlN2VhMDI0NjAwMjE1NGE4MmU3YzdlNWIwNDg2ZDhmODY5MjpzZXNzaW9uX2lkPTJfTVg0ME5UTXpNVFkwTW41LU1UUTBORFExTWprek5EZzNNSDR4VlRsT1ZYb3JXbk5rZG5sdWRXODVXSFpGYW5CbGRVaC1mZyZjcmVhdGVfdGltZT0xNDQ0NDUyOTM0Jm5vbmNlPTAuMTI1NDY3NDExMDA5NTk0OCZyb2xlPXB1Ymxpc2hlciZleHBpcmVfdGltZT0xNDQ1MDU3NzM0JmNvbm5lY3Rpb25fZGF0YT11c2VySWQlM0Q1NjE4ODg5NmY1MzRlMzc4MWFhNTc5OGQlM0JvcGVyYXRvcklkJTNENTYxODg4OTZmNTM0ZTM3ODFhYTU3OThk",
  "sessionId":"2_MX40NTMzMTY0Mn5-MTQ0NDQ1MjkzNDg3MH4xVTlOVXorWnNkdnludW85WHZFanBldUh-fg"
}
```


#### Response
```javascript
{
   "message":"ok"
}
```

## <a name='stream_received'>Stream received</a>

post /streams/streamreceived

```
#### Headers
```javascript
{
"Content-Type":"application/json",
"Authorization":"Bearer eyJ0eXAiOiJKV1QiLCJhbGciOiJIUzI1NiJ9.eyJhY2NvdW50SWQiOiI1NjAxMWUxOTdkYjJmNTZlMzU4ODdkNmYiLCJwZXJtaXNzaW9ucyI6W10sImlhdCI6MTQ0MjkxNDE0NiwiYXVkIjoiZHJvcGluLmNvbSIsImlzcyI6ImRyb3Bpbi5jb20ifQ.wt4P_elQAR8DIsLJPb8OENb8nfTb4aYdmEzu_3I8Hlk"
}
```
#### Body
```javascript
{
  "operatorId":"56188896f534e3781aa5798d",
  "token":"T1==cGFydG5lcl9pZD00NTMzMTY0MiZzaWc9NGM5YjdlN2VhMDI0NjAwMjE1NGE4MmU3YzdlNWIwNDg2ZDhmODY5MjpzZXNzaW9uX2lkPTJfTVg0ME5UTXpNVFkwTW41LU1UUTBORFExTWprek5EZzNNSDR4VlRsT1ZYb3JXbk5rZG5sdWRXODVXSFpGYW5CbGRVaC1mZyZjcmVhdGVfdGltZT0xNDQ0NDUyOTM0Jm5vbmNlPTAuMTI1NDY3NDExMDA5NTk0OCZyb2xlPXB1Ymxpc2hlciZleHBpcmVfdGltZT0xNDQ1MDU3NzM0JmNvbm5lY3Rpb25fZGF0YT11c2VySWQlM0Q1NjE4ODg5NmY1MzRlMzc4MWFhNTc5OGQlM0JvcGVyYXRvcklkJTNENTYxODg4OTZmNTM0ZTM3ODFhYTU3OThk",
  "sessionId":"2_MX40NTMzMTY0Mn5-MTQ0NDQ1MjkzNDg3MH4xVTlOVXorWnNkdnludW85WHZFanBldUh-fg"
}
```


#### Response
```javascript
{
   "message":"ok"
}
```

## <a name='stream_finished'>Stream finished</a>

post /streams//streamexit

```
#### Headers
```javascript
{
"Content-Type":"application/json",
"Authorization":"Bearer eyJ0eXAiOiJKV1QiLCJhbGciOiJIUzI1NiJ9.eyJhY2NvdW50SWQiOiI1NjAxMWUxOTdkYjJmNTZlMzU4ODdkNmYiLCJwZXJtaXNzaW9ucyI6W10sImlhdCI6MTQ0MjkxNDE0NiwiYXVkIjoiZHJvcGluLmNvbSIsImlzcyI6ImRyb3Bpbi5jb20ifQ.wt4P_elQAR8DIsLJPb8OENb8nfTb4aYdmEzu_3I8Hlk"
}
```
#### Body
```javascript
{
  "operatorId":"56188896f534e3781aa5798d",
  "userId":"54j5k43hj54k34354354l",
  "type":"operator" // ['viewer','operator'],
  "durationStreaming":"2323" //Seconds
  "distanceRouting":"32.4324" //Kilometres
}
```


#### Response
```javascript
{
   "operatorId":"56188896f534e3781aa5798d",
  "userId":"54j5k43hj54k34354354l",
  "price":"32132",
  "durationStreaming":"2323", //Seconds
  "distanceRouting":"32.4324",//Kilometres
  "ratingId":"43243243245fsgfdgf"
}
```


# <a name="Rating">Rating</a>
### <a name="rate_stream">Rate stream </a>


```javascript
post /streams/ratestream
```
#### Body
```javascript
{"type":"viewer",
 "ratingId":"56288ff5ae4b218c1daec071",
 "rate":"4",
 "videoUrl":"http://www.xxx.xyz"
 }
```
#### Response
```javascript
{
    "durationStreaming": "250",
    "distanceRouting": 0.01,
    "userId": "56287974cf8107681ba1ac1c",
    "operatorId": "56287b6d68f5e96bd5250116",
    "price": 4,
    "ratingId": "56289dcfae964ed81d8dd931"
}
```

