
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
  title: 'Stream has finished',
  durationStreaming: durationStreaming,
  distanceRouting: distanceRouting,
  price: price,
  ratingId: "432432432432432"
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
## Viewer list returned after operator adds location
```javascript

{
	code:7,
	messageId:'1234',
	message:'Viewer list'
	viewerIds: ['5453543543543543', '543543543543543543'] //list of channel of viewer.
}

```
## New operator return to viewer 
```javascript

{
	code:8,
	messageId:'1234',
	message:'New operator'
	operatorId: '5453543543543543' //channel name of operator,
	location:{
		longitude: '13.4343434343',
		latitude:  '12.3232323232'
	}
}

```
## New location for operator 
```javascript
	code: 9,
	messageId: '432423432432',
	operatorId: operatorId,
	location: {
		longitude:'43.434343',
		latitude:'34.43434343'
	},
	settingRadius:radius
```
## Switch operator to viewer
```javascript
	code: 10,
	operatorId: operatorId,
	messageId: '432423432432'
```
