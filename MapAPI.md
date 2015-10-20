
# NOTE: For manually testing, please add ?debug=true at the end each request made to get full info.
# dropin-doc



## [Map](#Map)

* [Get default location](#get_default_location)
* [Update new location to account](#add_new_location)
* [Search for operator](#search_for_operator)
* [Get profile of operator](#get_profile_operator)
* [Choose default operator](#choose_default_operator)
* [Request Operator](#request_operator)
* [Response Request](#response_request)
* [Get Oparator Location](#get_operator_location)
* [Remove location](#remove_location)
* [Set user (viewer/operator) online](#set_online)
* [Set user (viewer/operator) offline](#set_offline)


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
post /map/addlocation
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
  "latitude":50.24 //Float, REQUIRED,
  "settingRadius":50.22 //FLoat, REQUIRED
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
### <a name='search_for_operator'>Search for operators in 2,000m radius (default by server)</a>
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
  "longitude":40.24, //Float, REQUIRED
  "latitude":50.24 //Float, REQUIRED
}
```
#### Response
```javascript
[
    {
        "firstName": "hoa",
        "lastName": "nguyen",
        "archive": false,
        "status": "approved",
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
        "vendorId":Not yet generated, will update later, please use fake data, 
        "status":"unapproved"// ['unapproved', 'approved', 'banned', 'waiting','approved-first-time'], waiting: docusign not sent, unapproved: docusign is sent, but not signed, approved: docusign is signed, banned: operator is banned
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
  "longitude":40.24, //Float, REQUIRED
  "latitude":50.24 //Float, REQUIRED
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
### <a name='request_operator'>Request Operator</a>

Request operator for streaming a location

```javascript
post /map/operators/:accountId/request
```
#### Headers
```javascript
{
"Content-Type":"application/json",
"Authorization":"Bearer eyJ0eXAiOiJKV1QiLCJhbGciOiJIUzI1NiJ9.eyJhY2NvdW50SWQiOiI1NjAxMWUxOTdkYjJmNTZlMzU4ODdkNmYiLCJwZXJtaXNzaW9ucyI6W10sImlhdCI6MTQ0MjkxNDE0NiwiYXVkIjoiZHJvcGluLmNvbSIsImlzcyI6ImRyb3Bpbi5jb20ifQ.wt4P_elQAR8DIsLJPb8OENb8nfTb4aYdmEzu_3I8Hlk"
}
```
#### Params
- `accountId`: The requestor id

#### Body
```javascript
{
  "operatorId": 1, // Operator Id, REQUIRED
  "longitude":40.24, //Float, REQUIRED
  "latitude":50.24 //Float, REQUIRED
}
```
#### Response
```javascript
{
    "message": "Success message"
}
```

#### Push message to operator
```javascript
{
    "code": 4,
    "title": "Request for streaming",
    "location": { "long":40.24, "lat":50.24 }, // the request location
    "id": "5608b452dbb0a09419db1d1a", // ID of requestor
    "firstName": "Trinh", // First name of requestor
    "lastName": "Thai" // last name of requestor
}
```

### <a name='response_request'>Response Request</a>

Response to streaming request.

```javascript
post /map/operators/:opearatorId/response
```
#### Headers
```javascript
{
"Content-Type":"application/json",
"Authorization":"Bearer eyJ0eXAiOiJKV1QiLCJhbGciOiJIUzI1NiJ9.eyJhY2NvdW50SWQiOiI1NjAxMWUxOTdkYjJmNTZlMzU4ODdkNmYiLCJwZXJtaXNzaW9ucyI6W10sImlhdCI6MTQ0MjkxNDE0NiwiYXVkIjoiZHJvcGluLmNvbSIsImlzcyI6ImRyb3Bpbi5jb20ifQ.wt4P_elQAR8DIsLJPb8OENb8nfTb4aYdmEzu_3I8Hlk"
}
```
#### Params
- `opearatorId`: The operator id

#### Body
```javascript
{
  "requestor": 1, // The requestor id response to, REQUIRED
  "action": "accept",   // Either 'accept' or 'reject' REQUIRED
  "message": "response message", // The response message, OPTIONAL
}
```
#### Response
```javascript
{
    "message": "Success message"
}
```

#### Push message to viewer
```javascript
{
    "action": "accept", // Either 'accept' or 'reject'
    "code": 5,
    "message": "Hoa accepted your request", // Message from operator
    "title": "Request for streaming",
    "id": "5608b452dbb0a09419db1d1a", // ID of operator
    "firstName": "Trinh", // First name of operator
    "lastName": "Thai" // last name of operator
}
```

### <a name='get_operator_location'>Get Oparator Location</a>

Get operator location. Call this API within interval time to track operator location after get accepted

```javascript
get /map/operators/:operatorId/location
```
#### Headers
```javascript
{
"Content-Type":"application/json",
"Authorization":"Bearer eyJ0eXAiOiJKV1QiLCJhbGciOiJIUzI1NiJ9.eyJhY2NvdW50SWQiOiI1NjAxMWUxOTdkYjJmNTZlMzU4ODdkNmYiLCJwZXJtaXNzaW9ucyI6W10sImlhdCI6MTQ0MjkxNDE0NiwiYXVkIjoiZHJvcGluLmNvbSIsImlzcyI6ImRyb3Bpbi5jb20ifQ.wt4P_elQAR8DIsLJPb8OENb8nfTb4aYdmEzu_3I8Hlk"
}
```
#### Params
- `operatorId`: The operator id

#### Response
```javascript
{
    "lastTime": "2015-09-23T07:20:56.108Z",
    "latitude": 12343.56,
    "longitude": 1243.56
}
```

### <a name='remove_location'>Remove location</a>
Remove location of operator. Call this API when user logout.

```javascript
delete /map/operators/:operatorId/location
```
#### Headers
```javascript
{
"Content-Type":"application/json",
"Authorization":"Bearer eyJ0eXAiOiJKV1QiLCJhbGciOiJIUzI1NiJ9.eyJhY2NvdW50SWQiOiI1NjAxMWUxOTdkYjJmNTZlMzU4ODdkNmYiLCJwZXJtaXNzaW9ucyI6W10sImlhdCI6MTQ0MjkxNDE0NiwiYXVkIjoiZHJvcGluLmNvbSIsImlzcyI6ImRyb3Bpbi5jb20ifQ.wt4P_elQAR8DIsLJPb8OENb8nfTb4aYdmEzu_3I8Hlk"
}
```
#### Params
- `operatorId`: The operator id

#### Response
Deleted location
```javascript
{
    "lastTime": "2015-09-23T07:20:56.108Z",
    "latitude": 12343.56,
    "longitude": 1243.56
}
```

## <a name='set_online'>Set a user to online</a>

```javascript
post /map/setonline
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
    "message":"ok"
}
```


## <a name='set_offline'>Set a user to offline</a>

```javascript
post /map/setoffline
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
    "message":"ok"
}
```
