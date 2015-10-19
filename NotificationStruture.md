
# Notification structure



## Stream has been started from droperator
```javascript
{
   code: 2,
   messageId:'1234',
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
messageId:'1234',
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

## Response from the droperator for the requested stream
```javascript
{
   code:5
   id: operatorId,
   firstName:"Hoa",
   messageId:'1234',
   lastName:"Nguyen",
   title:"Request for streaming",
   action:'accept' or 'deny',
   message:'accepted from ....'
}
```
## Stream finished (both sent to operator and viewer)
```javascript

{
  code: 3,
  messageId:'1234',
  userId: viewerId/operatorId,
  title: 'Stream has finished'
}
```
## DocuSign Approved
```javascript

{
	code:6,
	messageId:'1234',
	title:'DocuSign Form Approved!',
	message:'DocuSign Form Approved!'
}

```
