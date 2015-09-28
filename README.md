# NOTE: For manually testing, please add ?debug=true at the end each request made to get full info.
# dropin-doc
## [Registration](#Registration)

* [Create new account](#new_account)

## [Authorization](#Authorization)

* [Login](#login)
* [Verify](#verify)

## [Device](#Device)

* [Add new device](#new_device)

## [Notification](#Notification)

* [Send notification](#send_notification)

## [Map](#Map)

* [Get default location](#get_default_location)
* [Update new location to account](#add_new_location)
* [Search for operator](#search_for_operator)
* [Get profile of operator](#get_profile_operator)
* [Choose default operator](#choose_default_operator)

## [Profile](#Profile)

* [Update account profile](#update_account_profile)

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
  "code":"0643", //String, REQUIRED
  "deviceAddress": "APA91bF4S5VIv9bg8katkkkh_4XJxI8j0efT5Dodgf95fVUSVsWbKZGyHgLwvOooJn1I-yjgbht91dM0yvSHqiY_l-a1No6gY9_2tQbUropwzrBfAcJCDgYlqQCxiSmEWJY8nataDmAy",
  "deviceType":"android" // ['android','ios']
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
    "deviveType":"android" //String, REQUIRED ['android', 'ios']
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

## <a name="Map">Map</a>
### <a name='get_default_location'>Get default location</a>
```javascript
post /map/location/default
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
   
  "lat":40.24,
  "lng":50.24
  
}
```
### <a name='add_new_location'>Add new location to account</a>
```javascript
post /map
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
  "longitude":40.24, //Float, REQUIRED
  "latitude":50.24 //Float, REQUIRED
}
```
#### Response
```javascript
{
    "latitude": 123,
    "longitude": 123456,
    "account": "5601274dd47400694e8c0682",
    "archive": false,
    "visibility": "private",
    "type": "real",
    "createdAt": "2015-09-23T07:58:19.667Z",
    "updatedAt": "2015-09-23T07:58:19.667Z",
    "id": "56025b9b4f19fd534de2fc28"
}
```
### <a 'name='search_for_operator>Search for operators in 2,000m radius (default by server)</a>
```javascript
get /map/operators
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
  "long":40.24, //Float, REQUIRED
  "lat":50.24 //Float, REQUIRED
}
```
#### Response
```javascript
[
    {
        "firstName": "hoa",
        "lastName": "nguyen",
        "archive": false,
        "status": "active",
        "type": "user",
        "createdAt": "2015-09-22T08:49:46.021Z",
        "updatedAt": "2015-09-22T08:49:46.033Z",
        "id": "5601162a04bff45c1cc93ca7",
        "location": {
            "lastTime": "2015-09-23T07:20:56.108Z",
            "latitude": 1234.56,
            "longitude": 124.56
        }
    },
    {
        "firstName": "hoa1",
        "lastName": "nguyen1",
        "archive": false,
        "status": "active",
        "type": "user",
        "createdAt": "2015-09-22T08:49:46.021Z",
        "updatedAt": "2015-09-22T08:49:46.033Z",
        "id": "5601162a04bff45c1cc93ca7",
        "location": {
            "lastTime": "2015-09-23T07:20:56.108Z",
            "latitude": 12343.56,
            "longitude": 1243.56
        }
    }
]
```
### <a name='get_profile_operator'>Get profile of operator</a>
```javascript
get /map/operators/profile
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
  "accountId":"4gfdgfddfdfdf", //String, REQUIRED
}
```
#### Response
```javascript
{
    "account": {
        "firstName": "hoa",
        "lastName": "nguyen",
        "archive": false,
        "status": "active",
        "type": "user",
        "createdAt": "2015-09-28T03:30:26.212Z",
        "updatedAt": "2015-09-28T03:30:26.219Z",
        "id": "5608b452dbb0a09419db1d1a"
    },
    "operator": {
        "account": "5608b452dbb0a09419db1d1a",
        "createdAt": "2015-09-28T03:53:07.786Z",
        "taxFormId":Not yet generated, will update later, please use fake data,
        "vendorId":Not yet generated, will update later, please use fake data
        "updatedAt": "2015-09-28T03:53:07.786Z",
        "id": "5608b9a34e8a66640c369df9"
    }
}
```
### <a name='choose_default_operator'>Choose default operator</a>
```javascript
post /map/operators/choosedefault
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
  "long":40.24, //Float, REQUIRED
  "lat":50.24 //Float, REQUIRED
}
```
#### Response
```javascript
{
    "firstName": "hoa",
    "lastName": "nguyen",
    "archive": false,
    "status": "active",
    "type": "user",
    "createdAt": "2015-09-28T03:22:42.644Z",
    "updatedAt": "2015-09-28T03:22:42.657Z",
    "id": "5608b282c0dc92481bd93c5d",
    "location": {
        "key": "5608b282c0dc92481bd93c5d",
        "latitude": 14.00000050663948,
        "longitude": 14.000001847743988,
        "distance": 1080
    }
}
```
## <a name="Profile">Profile</a>

### Note: Body *id* must match with params *id*

### <a name='update_account_profile'>Update account</a>
```javascript
Patch /accounts/:accountId
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
