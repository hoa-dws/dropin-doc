
# Notification structure

## Stream has been started from droperator
```javascript
{
   code: 2,
   operatorId: operatorId,
   token: token,
   apiKey: opentokConfig.apiKey,
   sessionId: sessionId
}
```
## Stream has been requested from viewer
```javascript
{
code:4
id: viewerId,
firstName:"Hoa",
lastName:"Nguyen",
title:"Request for streaming",
location:
   {
        longitude:12,
        latitude: 14
   }
}
```
