# Update Delivery Note

Update fields of the delivery note. (Currently only the state can be changed!)

**URL** : `/delivery_note/{id}`

**Method** : `PATCH`

## Headers

In order for the request to work the following header is necessary: <br>

**Content-Type** : `application/json`

## Url

The 'id' property of the url will be used to identify the delivery note to patch. <br>
This is the id returned by the previous POST Delivery Note request.

## Payload

The payload is a json in the body. <br>
Currently only the field 'state' is supported. <br>
Only the values 'c' or 'canceled' are accepted as a valid state. <br>
All other payload properties will have no impact and return an '400 Bad Request' error.

**Payload example**

```json
{
  "state": "canceled"
}
```

## Success Response

**Code** : `200 OK`

If the request was valid there will be a response json with the patched data.
If the request is only partially correct and the validation fails, nothing will be patched.

**Response example**

```json
{
  "id": "3417",
  "state": "canceled"
}
```

## Failure Response

**Code** : `400 Bad Request`

Will be returned if:
- There is no delivery note for given id
- There is no valid property to patch
- There is no valid value to patch

**Content examples**

```json
{
  "error_code": 400,
  "message": "No delivery note found for given id!"
}
```


```json
{
  "error_code": 400,
  "message": "No valid property found to patch!"
}
```

```json
{
  "error_code": 400,
  "message": "No valid value was given to patch!"
}
```

**Code** : '409 Conflict'

There was an error with the intern mapping. Please contact support@reebuild.com with the payload, so we can fix this asap. 

**Code** : '500 Internal Server Error'

There was an unexpected error. Please contact support@reebuild.com with the payload, so we can fix this asap. 
