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
| params  | required  | type |
| :------------: |:---------------:| :-----:|
| email      | true | string |
| phone     | true        |   string |


#### Response

| params  |  type |
| :------------:|:-----:|
| account     | string |
| code      | string |
| expiredOn      | date |
| createdAt      | date |
| updatedAt      | date |


### Verify token
```javascript
post /verify
```
#### Body
| params  | required  | type |
| :------------: |:---------------:| :-----:|
| code     | true | string |


#### Response
Token object with infomation


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
      "value": "123456", //String, REQUIRED
      "type": "phone" //String, REQUIRED
    },
    {
      "value": "abcdef", //String, REQUIRED
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
        "code": "4478",
        "createdAt": "2015-09-22T09:23:37.517Z",
        "updatedAt": "2015-09-22T09:23:37.517Z",
        "id": "56011e197db2f56e35887d72"
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
### Add new device 
```javascript
post /adddevice
```
#### Prerequisite: User already login
#### Body
| params  | required  | type |
| :------------: |:---------------:| :-----:|
| deviceAddress      | true | string |
| deviceType     | true        |   string |


#### Response
* OK: Status 200
* Failed: Status 400 or 500

### Remove device 
```javascript
post /removedevice
```
#### Prerequisite: User already login
#### Body
| params  | required  | type |
| :------------: |:---------------:| :-----:|
| deviceAddress      | true | string |


#### Response
* OK: Status 200
* Failed: Status 400 or 500

