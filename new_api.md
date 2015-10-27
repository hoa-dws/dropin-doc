# Controllers

Controllers expose Drop-In's REST API.

## API

* REST calls require the Content-type header to be application/json
* REST calls require the Accept-encoding header to be application/json
* If a call request Authentication, the auth_token parameter (with a valid JWT code) needs to be either passed into the URL query or into the request body.
* Due to the JWT requirement, ALL calls must be done via HTTPS.  All HTTP calls to the API will be rejected as forbidden.
* If the REST API request fails, it will return the appropriate HTTP code as well as an array of Error objects.  (Made up of code string, a message string, and a data array of additional details about the error)
* If the client REST library does not support HTTP PATCH calls, you can pass ``x-http-method-override`` set as ``patch`` into the header of a PUT request and the server will treat it as a PATCH request.

## References

* API Security: https://stormpath.com/blog/the-ultimate-guide-to-mobile-api-security/ (Archive: https://archive.is/9aIYG)
* JSON PATCH spec: http://tools.ietf.org/html/rfc6902 (Archive: https://archive.is/KaXpR)
* Language codes: http://www.loc.gov/standards/iso639-2/php/code_list.php (Archive: https://archive.is/IS3b)
* Country codes: https://en.wikipedia.org/wiki/ISO_3166-1_alpha-2 (Archive: https://archive.is/9P0Cm)
* JSON Web Tokens: https://tools.ietf.org/html/rfc7519 (Archive: https://archive.is/fuwxO)

# Actions

- [Account](#account)
    - [Response](#response)
    - [POST /accounts](#post-accounts)
        - [CURL](#curl)
        - [Response](#response)
    - [GET /accounts](#get-accounts)
        - [CURL](#curl)
        - [Response](#response)
    - [GET /accounts/**<accountId>**](#get-accountsaccountid)
        - [CURL](#curl)
        - [Response](#response)
    - [PATCH /accounts/**<accountId>**](#patch-accountsaccountid)
        - [CURL](#curl)
        - [Response](#response)
    - [DELETE /accounts/**<accountId>**](#delete-accountsaccountid)
        - [CURL](#curl)
        - [Response](#response)
- [Authentication](#authentication)
    - [POST /login](#post-login)
        - [Response](#response)
        - [CURL](#curl)
    - [POST /login/verify](#post-loginverify)
        - [Response](#response)
        - [CURL](#curl)
- [Devices](#devices)
    - [Response](#response)
    - [POST /devices](#post-devices)
        - [CURL](#curl)
        - [Response](#response)
    - [DELETE /devices/**<deviceId>**](#delete-devicesdeviceid)
        - [CURL](#curl)
        - [Response](#response)
- [Notifications](#notifications)
    - [Response](#response)
    - [PATCH /notifications](#patch-notifications)
        - [CURL](#curl)
        - [Response](#response)
    - [GET /notifications](#get-notifications)
        - [CURL](#curl)
        - [Response](#response)
- [Payments](#payments)
- [CDN](#cdn)
- [Map](#map)
    - [POST /map](#post-map)
        - [Response](#response)
        - [CURL](#curl)
    - [GET /map](#get-map)
        - [Response](#response)
- [Gig](#gig)
    - [Response](#response)
    - [GET /gigs](#get-gigs)
        - [CURL](#curl)
        - [Response](#response)
    - [GET /gigs/**<gigId>**](#get-gigsgigid)
        - [CURL](#curl)
        - [Response](#response)
    - [POST /gigs](#post-gigs)
        - [CURL](#curl)
    - [Response](#response)
    - [POST /gigs/**<gigId>**/claim](#post-gigsgigidclaim)
        - [CURL](#curl)
        - [Response](#response)
    - [POST /gigs/**<gigId>**/confirm](#post-gigsgigidconfirm)
        - [CURL](#curl)
        - [Response](#response)
    - [POST /gigs/**<gigId>**/start](#post-gigsgigidstart)
        - [CURL](#curl)
        - [Response](#response)
    - [POST /gigs/**<gigId>**/stop](#post-gigsgigidstop)
        - [CURL](#curl)
        - [Response](#response)
- [Streams](#streams)
- [PaymentOptions](#paymentoptions)
- [Ratings](#ratings)
- [DocuSign](#docusign)

# Account

Accounts contain user information and access permission data.

## Response

Successful POST, GET, and PATCH requests will return an Account Object:

|Field|Description|Type|Role Visibility|
|:----|:----------|:--:|:--------------|
|id|ID|String|All|
|createdAt|Creation datetime|Date|Self|
|updatedAt|Last updated datetime|Date|Self|
|type|Last updated datetime|Date|Self, Customer|
|status|Last updated datetime|Date|Self, Customer|
|firstName|First name|String|Self, Customer|
|lastName|Last name|String|Self, Customer|
|city|City|String|Self, Customer|
|state|State/region/province/prefecture name|String|Self, Customer|
|country|Two-digit ISO 3166-1 country code|String|Self, Customer|
|language|Two/three-digit ISO 639.2 language code|String|Self, Customer|
|identities|Collection of account identities|Array<Identity>|Self|
|identities[n].type|The type of identity attached to the account ('phone','email')|String|Self|
|identities[n].value|The value of the identity (E-mail address or phone number)|String|Self|
|operator|Operator information|Object|Self, Customer|
|operator.vendorId|The Bill.com vendor ID of the operator|String|Self|
|operator.taxFormId|The DocuSign ID of the operator's 1099|String|Self|
|operator.status|The Operator's status ('unapproved', 'approved', 'banned', 'waiting')|String|Self, Customer|

## POST /accounts

Adds a DropIn Account

|Field|Description|Type|Required|Default|Role Access|
|:----|:----------|:--:|:------:|:-----:|:---------:|
|firstName|First name|String|true|undefined|All|
|lastName|Last name|String|true|undefined|All|
|city|City|String|false|undefined|All|
|state|State/region/province/prefecture name|String|false|undefined|All|
|country|Two-digit ISO 3166-1 country code|String|false|undefined|All|
|language|Two/three-digit ISO 639.2 language code|String|false|undefined|All|
|identities|Collection of account identities|Array<Identity>|true|[]|All|
|identities[n].type|The type of identity attached to the account ('phone','email')|String|true|undefined|All|
|identities[n].value|The value of the identity (E-mail address or phone number)|String|true|undefined|All|

### CURL

```curl -XPOST -H 'Accept-encoding: application/json' -H "Content-type: application/json" -d '{ "firstName": "test", "lastName": "test", "identities": [ { "type": "email", "value": "test@test.com" }, { "type": "phone", "value": "5551234567" } ]}' 'https://localhost/accounts'```

### Response

Account Object

## GET /accounts

Searches DropIn Accounts based on criteria:

|Field|Description|Type|Required|Default|Role Access|
|:----|:----------|:--:|:------:|:-----:|:---------:|
|firstName|First name|String|true|undefined|All|
|lastName|Last name|String|true|undefined|All|
|city|City|String|false|undefined|All|
|state|State/region/province/prefecture name|String|false|undefined|All|
|country|Two-digit ISO 3166-1 country code|String|false|undefined|All|
|language|Two/three-digit ISO 639.2 language code|String|false|undefined|All|
|identities|Collection of account identities|Array<Identity>|true|[]|All|
|identities[n].type|The type of identity attached to the account ('phone','email')|String|true|undefined|All|
|identities[n].value|The value of the identity (E-mail address or phone number)|String|true|undefined|All|
|start|The index within the results array to start returning|Integer|false|0|All|
|limit|How many results to return|Integer|false|0|All|
|sort|Sorting instructions in 'field DIRECTION' format|String|false|'id DESC'|All|

### CURL

```curl -XGET -H 'Accept-encoding: application/json' -H "Content-type: application/json" -d '{ "firstName": "test", "lastName": "test" }' 'https://localhost/accounts'```

### Response

Array of Account Objects

## GET /accounts/**<accountId>**

Searches DropIn Accounts based on an **<accountId>**.

### CURL

```curl -XGET -H 'Accept-encoding: application/json' -H "Content-type: application/json" 'https://localhost/accounts/1'```

### Response

Account Object

## PATCH /accounts/**<accountId>**

Adds a DropIn Account

|Field|Description|Type|Required|Default|Role Access|
|:----|:----------|:--:|:------:|:-----:|:---------:|
|firstName|First name|String|false|undefined|Self|
|lastName|Last name|String|false|undefined|Self|
|city|City|String|false|undefined|Self|
|state|State/region/province/prefecture name|String|false|undefined|Self|
|country|Two-digit ISO 3166-1 country code|String|false|undefined|Self|
|language|Two/three-digit ISO 639.2 language code|String|false|undefined|Self|
|identities|Collection of account identities|Array<Identity>|false|[]|Self|
|identities[n].op|Should be set to ``'update'``|false|undefined|Self|
|identities[n].type|Instructions on how to transform an entry|Object|false|undefined|Self|
|identities[n].value.id|The ID of the record within the collection that needs to be transformed|String|false|undefined|All|
|identities[n].value.type|The type of identity attached to the account ('phone','email')|String|false|undefined|All|
|identities[n].value.value|The value of the identity (E-mail address or phone number)|String|true|undefined|Self|

### CURL

```curl -XPATCH -H 'Accept-encoding: application/json' -H "Content-type: application/json" -d '{ "firstName": "test", "lastName": "test" }' 'https://localhost/accounts/1'```

### Response

Account Object

## DELETE /accounts/**<accountId>**

Archives a DropIn Account

### CURL

```curl -XDELETE -H 'Accept-encoding: application/json' -H "Content-type: application/json" 'https://localhost/accounts/1'```

### Response

``true``

# Authentication

Authenticates DropIn Account credentials and manages JSON Web Tokens

## POST /login

Confirms DropIn Account credentials and generates an Access Token

|Field|Description|Type|Required|Default|Role Access|
|:----|:----------|:--:|:------:|:-----:|:---------:|
|email|Email Address|String|true|undefined|All|
|phone|Phone Number|String|true|undefined|All|

### Response

|Field|Description|Type|Role Visibility|
|:----|:----------|:--:|:--------------|
|token|Access token ID|String|All|
|account|Account Object|Account|All|
|code|Access token code (**Development environments only**)|String|All|

### CURL

```curl -XPOST -H 'Accept-encoding: application/json' -H "Content-type: application/json" -d '{ "phone": "5551234567", "email": "test@test.com" }' 'https://localhost/login'```

## POST /login/verify

Verifies the DropIn account is attached to a phone

|Field|Description|Type|Required|Default|Role Access|
|:----|:----------|:--:|:------:|:-----:|:---------:|
|tokenId|Access Token ID|String|true|undefined|All|
|code|Access Token code|String|true|undefined|All|

### Response

|Field|Description|Type|Role Visibility|
|:----|:----------|:--:|:--------------|
|token|JSON Web Token hash|String|All|
|account|Account Object|Account|All|

### CURL

```curl -XPOST -H 'Accept-encoding: application/json' -H "Content-type: application/json" -d '{ "tokenId": "1", "code": "7392" }' 'https://localhost/login/verify'```

# Devices

Accounts contain user information and access permission data.

## Response

Successful POST requests will return the following Device Objects:

|Field|Description|Type|Role Visibility|
|:----|:----------|:--:|:--------------|
|id|ID|String|All|
|createdAt|Creation datetime|Date|Self|
|updatedAt|Last updated datetime|Date|Self|
|type|Device type|String|Self, Customer|
|address|Device address|String|Self, Customer|

## POST /devices

Adds a device to a DropIn Account

|Field|Description|Type|Required|Default|Role Access|
|:----|:----------|:--:|:------:|:-----:|:---------:|
|address|Device address|String|true|undefined|Self|
|type|Device type|String|true|undefined|Self|

### CURL

```curl -XPOST -H 'Accept-encoding: application/json' -H "Content-type: application/json" -d '{ "address": "???", "type": "???" }' 'https://localhost/devices'```

### Response

Device Object

## DELETE /devices/**<deviceId>**

Archives a device

### CURL

```curl -XDELETE -H 'Accept-encoding: application/json' -H "Content-type: application/json" 'https://localhost/devices/1'```

### Response

true

# Notifications

Notifications a DropIn Account receives.

## Response

Successful GET and PATCH requests will return the following Notification Object:

|Field|Description|Type|Role Visibility|
|:----|:----------|:--:|:--------------|
|id|ID|String|All|
|createdAt|Creation datetime|Date|Self|
|updatedAt|Last updated datetime|Date|Self|
|type|Notification type ('read','unread')|String|Self|
|status|The status of the notification. ('pending', 'sent', 'failed', 'received')|String|Self|
|sender|The Account Object of the sender|Account|Self|
|recipient|The Account Object of the recipient|Account|Self|
|title|Title|String|Self|
|message|Message|String|Self|

## PATCH /notifications

Updates a Notification

|Field|Description|Type|Required|Default|Role Access|
|:----|:----------|:--:|:------:|:-----:|:---------:|
|type|Change notification type. ('read','unread')|String|true|undefined|Self|

### CURL

```curl -XPATCH -H 'Accept-encoding: application/json' -H "Content-type: application/json" -d '{ "type": "unread" }' 'https://localhost/notifications/1'```

### Response

Notification Object

## GET /notifications

Searches DropIn Accounts based on criteria:

|Field|Description|Type|Required|Default|Role Access|
|:----|:----------|:--:|:------:|:-----:|:---------:|
|id|ID|String|false|undefined|All|
|createdAt|Creation datetime|Date|false|undefined|Self|
|updatedAt|Last updated datetime|Date|false|undefined|Self|
|type|Notification type ('read','unread')|String|false|undefined|Self|
|sender|The Account Object of the sender|Account|false|undefined|Self|
|recipient|The Account Object of the recipient|Account|false|undefined|Self|
|title|Title|String|false|undefined|Self|
|message|Message|String|false|undefined|Self|

### CURL

```curl -XGET -H 'Accept-encoding: application/json' -H "Content-type: application/json" -d '{ "status": "read" }' 'https://localhost/notifications'```

### Response

Arrary of Notification Objects

# Payments

Coming soon!

# CDN

Coming soon!

# Map

## POST /map

Updates the DropIn map with an Account's location.

|Field|Description|Type|Required|Default|Role Access|
|:----|:----------|:--:|:------:|:-----:|:---------:|
|lat|Email Address|Float|true|undefined|All|
|lng|Phone Number|Float|true|undefined|All|
|bty|Battery remaining|Integer|true|undefined|All|
|sig|Signal strength|Integer|true|undefined|All|
|opr|Is Account Operator?|Boolean|true|undefined|All|
|net|Network type (0 = 2G, 1 = G, 2 = E, 3 = 3G, 4 = H, 5 = H+6, 6 = H+7, 7 = H+8, 8 = H+9, 9 = H+10, 10 = 4GLTE, 11 = 4GLTE-A)|Integer|true|undefined|All|

### Response

true

### CURL

```curl -XPOST -H 'Accept-encoding: application/json' -H "Content-type: application/json" -d '{ "lat": 0.012, "lng": 0.012, "bty": 100, "sig": 50, "opr" true, "net": 1 }' 'https://localhost/map'```

## GET /map

Searches the DropIn Map for Droperators near a location, sorted by closest proximity.

|Field|Description|Type|Required|Default|Role Access|
|:----|:----------|:--:|:------:|:-----:|:---------:|
|lat|Latitude to search around|String|true|undefined|All|
|long|Longitude to search around|String|true|undefined|All|
|radius|Radius to search within|String|false|undefined|All|

### Response

An array (sorted by a ranking algorithm) of:

|Field|Description|Type|Role Visibility|
|:----|:----------|:--:|:--------------|
|[n].account|Account Object of the Droperator|Account|All|
|[n].location|Location data of the Droperator|Object|All|
|[n].location.latitude|Latitude of the Droperator|String|All|
|[n].location.longitude|Longitude of the Droperator|String|All|

# Gig

DropIn Gigs between Customers and Operators

## Response

Successful GET and plain POST requests will return the following Gig Object:

|Field|Description|Type|Role Visibility|
|:----|:----------|:--:|:--------------|
|id|ID|String|All|
|createdAt|Creation datetime|Date|Self|
|updatedAt|Last updated datetime|Date|Self|
|type|Gig type ('test','real')|String|Self|
|status|The status of the gig. ('pendingOperator', 'operatorFound', 'operatorEnroute', 'streaming', 'purchased', 'voted', 'invoiced', 'compensated', 'expired', 'failed')|String|Self|
|reconnectionAttempts|Integer|Self|
|duration|Duration of the gig in seconds|Integer|Self|
|stream|Stream Object of the Gig|Stream|Self|
|customer|Account Object of the customer|Account|Self|
|operator|Account Object of the droperator|Account|Self|
|customerRating|Rating Object the operator gave the customer|Rating|Self|
|operatorRating|Rating Object the customer gave the operator|Rating|Self|
|latitude|Latitude of the Gig|String|Self|
|longitude|Longitude of the Gig|String|Self|

## GET /gigs

Searches Gigs based on criteria:

|Field|Description|Type|Required|Default|Role Access|
|:----|:----------|:--:|:------:|:-----:|:---------:|
|id|ID|String|false|undefined|All|
|status|The status of the notification. ('pendingOperator', 'operatorFound', 'operatorEnroute', 'streaming', 'purchased', 'voted', 'invoiced', 'compensated', 'expired', 'failed')|String|false|undefined|Self|
|duration|Duration of the gig in seconds|Integer|false|undefined|Self|
|stream|Stream Object of the Gig|Stream|false|undefined|Self|
|customer|Account Object of the customer|Account|false|undefined|Self|
|operator|Account Object of the droperator|Account|false|undefined|Self|
|customerRating|Rating Object the operator gave the customer|Rating|false|undefined|Self|
|operatorRating|Rating Object the customer gave the operator|Rating|false|undefined|Self|
|latitude|Latitude of the Gig|String|false|undefined|Self|
|longitude|Longitude of the Gig|String|false|undefined|Self|
|start|The index within the results array to start returning|Integer|false|0|All|
|limit|How many results to return|Integer|false|0|All|
|sort|Sorting instructions in 'field DIRECTION' format|String|false|'id DESC'|All|

### CURL

```curl -XGET -H 'Accept-encoding: application/json' -H "Content-type: application/json" -d '{ "status": "voted", "duration": 60 }' 'https://localhost/gigs'```

### Response

Gig Object

## GET /gigs/**<gigId>**

Searches Gigs based on an **<gigId>**.

### CURL

```curl -XGET -H 'Accept-encoding: application/json' -H "Content-type: application/json" 'https://localhost/gigs/1'```

### Response

Array of Gig Objects

## POST /gigs
  
Creates a Gig Object

|Field|Description|Type|Required|Default|Role Access|
|:----|:----------|:--:|:------:|:-----:|:---------:|
|latitude|Latitude of the gig|String|true|undefined|All|
|longitude|Longitude of the gig|String|true|undefined|All|

### CURL

```curl -XPOST -H 'Accept-encoding: application/json' -H "Content-type: application/json" -d '{ "latitude": "1.02", "longitude": "1.03" }' 'https://localhost/gigs'```

## Response

|Field|Description|Type|Role Visibility|
|:----|:----------|:--:|:-------------:|
|gig|Gig Object|Gig|Self, Customer|
|purchaseToken|BrainTree access token for the customer|String|Self, Customer|

## POST /gigs/**<gigId>**/claim

Allows a Droperator to claim a Gig

|Field|Description|Type|Required|Default|Role Access|
|:----|:----------|:--:|:------:|:-----:|:---------:|
|response|A response type ('accept', 'reject')|String|true|undefined|All|

### CURL

```curl -XPOST -H 'Accept-encoding: application/json' -H "Content-type: application/json" -d '{ "response": "accept" }' 'https://localhost/gigs/1/claim'```

### Response

|Field|Description|Type|Role Visibility|
|:----|:----------|:--:|:-------------:|
|gig|Gig Object|Gig|Self, Customer|

## POST /gigs/**<gigId>**/confirm

Allows a Customer to confirm that they are ready to start a claimed Gig

|Field|Description|Type|Role Visibility|
|:----|:----------|:--:|:-------------:|
|paymentMethodNonce|A BrainTree nonce of a payment type to use for the gig|String|true|undefined|All|

### CURL

```curl -XPOST -H 'Accept-encoding: application/json' -H "Content-type: application/json" -d '{ "paymentMethodNonce": "lkjabshdliuhbvilsublsevsfvsaervrh" }' 'https://localhost/gigs/1/confirm'```

### Response

|Field|Description|Type|Role Visibility|
|:----|:----------|:--:|:-------------:|
|gig|Gig Object|Gig|Self, Customer|

## POST /gigs/**<gigId>**/start

Allows a Droperator to start the Gig once they are within range

### CURL

```curl -XPOST -H 'Accept-encoding: application/json' -H "Content-type: application/json" 'https://localhost/gigs/1/start'```

### Response

|Field|Description|Type|Role Visibility|
|:----|:----------|:--:|:-------------:|
|gig|Gig Object|Gig|Self, Customer|
|streamToken|OpenTok publisher token for the operator|String|Self, Customer|

## POST /gigs/**<gigId>**/stop

Allows a Droperator or Customer to stop a Gig

### CURL

```curl -XPOST -H 'Accept-encoding: application/json' -H "Content-type: application/json" 'https://localhost/gigs/1/stop'```

### Response

|Field|Description|Type|Role Visibility|
|:----|:----------|:--:|:-------------:|
|gig|Gig Object|Gig|Self, Customer|
|price|How much the gig cost|String|Self, Customer|

# Streams

Coming soon!

# PaymentOptions

Coming soon!

# Ratings

'get /ratings': 'RatingController.search',
  'get /ratings/:ratingId': 'RatingController.get',
  'post /ratings': 'RatingController.create',
  'put /ratings/:ratingId': 'RatingController.overwrite',
  'patch /ratings/:ratingId': 'RatingController.update',
  'delete /ratings/:ratingId': 'RatingController.archive',

# DocuSign

'post /docusign':'DocuSignController.hook',
  'get /docusign/status':'DocuSignController.checkDocuSignStatus',
  'post /docusign/send':'DocuSignController.sendDocuSign',
  'post /sendfeedback':'FeedbackController.sendFeedback'

---------------------------------
