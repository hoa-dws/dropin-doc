# dropin-doc
## [Registration](#Registration)
## [Authorization](#Authorization)
## <a name="Authorization">Authorization</a>
### Login with email
```javascript
post /login
```
#### Body
| params  | required  | type |
| :------------: |:---------------:| :-----:|
| email      | true | string: email |
| token     | true        |   string |

### Login with phone
```javascript
post /login
```
#### Body
| params  | required  | type |
| :------------: |:---------------:| :-----:|
| phone     | true | string |
| token      | true        |   string |

#### Response

| params  |  type |
| :------------:|:-----:|
| account     | string |
| code      | string |
| code      | ['unverified','verified','expired'] |
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
post /signup
```
#### Body
| params  | required  | type |
| :------------: |:---------------:| :-----:|
| firstName     | true | string |
| lastName     | true        |   string |
| street     | false        |   string |
| city     | false        |   string |
| state     | false        |   string |
| country     | false        |   string |
| language     | false        |   string |
| archive     | false        |   boolean |
| status     | false        |   ['active','banned'], default: 'active' |
| type    | false        |   ['robot', 'trial', 'user', 'consumer', 'tester', 'customerSupport', 'admin'], default: 'trial' |
| identities     | true        |   [{ObjectIdentity}] |

#### ObjectIndentity
 params  | required  | type |
| :------------: |:---------------:| :-----:|
| type     | true | ['email','phone','facebook','gmail','twitter','linkedin'] |
| value     | true        |   string |
| archive     | false        |   boolean |
| status     | false        |   ['unverified','verified','cancelled','expired'], default: 'unverified' |

#### Response
Newly created account object
