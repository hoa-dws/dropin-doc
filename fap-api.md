## [Fake api](#Fake api)
* [Update map for fake operator](#fake_update_map)
* [Remove fake location](#remove_fake_location)
## <a name="Fake api">Fake api</a>
### <a name="fake_update_map">Fake api update map </a>
```javascript
post /map/addfakelocation
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
  "latitude":12,
  "longitude":14
}

```

#### Response
```javascript
{
    "lat": 12,
    "long": 14
}
```
