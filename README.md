# dropin-doc
## [Registration](#Registration)
## [Authorization](#Authorization)
## [Device](#Device)
## <a name="Authorization">Authorization</a>
### Login with email
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
    "id": "56011ee57db2f56e35887d73" //Save this field for latter verification
}
```
### Verify token
```javascript
post /login/verify
```
#### Body
```javascript
{
  "tokenId":"56011ee57db2f56e35887d73",
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
## <a name="Registration">Registration</a>
### Create new account
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
        "id": "56011e197db2f56e35887d72" //Save this field for latter verification
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

## <a name="Device">Device</a>
### Add new device to an account
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

### Send notification (currently working on android only, ios needs to implement accordingly to work)
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
  "recipientId":"5560122297db2f56e35887d76", //id of account to send
  "message":"Test"
}
```

#### Response
* OK: Status 200
* Failed: Status 400 or 500

