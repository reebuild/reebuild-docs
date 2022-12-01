# Update Delivery Note

This endpoint is used to make changes to delivery notes. <br>
The only unlocked operation is to change the state. <br>
It can only be set to canceled if the given delivery note has not been signed yet. <br>

**URL** : `https://api.reebuild.com/industry/customer_connection/delivery_note/<deliveryNoteId>`

**Method** : `PATCH`

## Headers

The following headers must be set: <br>

**Content-Type** : `application/json`

**Api-Key¹** : `<api-key>`

¹ You receive the API-Key in the course of the OnBoarding by mail.

## Url Parameter

The `deliveryNoteId` url section is used to identify your incorrect delivery bill. <br>
When replacing the `deliveryNoteId` value, please remove the angle brackets.

## Payload

The payload is a [JSON](https://en.wikipedia.org/wiki/JSON) in the body. <br>
Currently only the field `state` is supported. <br>
There is only one allowed value: `CANCELLED` <br>

## Example

**URL** : `https://api.reebuild.com/industry/customer_connection/delivery_note/LS2649G34` <br> <br>
**Payload** :
```json
{
  "state": "CANCELLED"
}
```

## Success Response

**Code** : `200 OK`

If the request is successful, the new set values are transmitted as response.

**Response example**

```json
{
  "state": "CANCELLED"
}
```

## Failure Response

**Code** : `400 Bad Request`

Is sent as a response if one of the following criteria is true:
- An invalid value was passed to the endpoint
- The value could not be set, due to restrictions <br>(e.g.: The delivery note is already signed)

**Content examples**

```json
{
  "error_code": 400,
  "message": "No valid value was given to patch!",
  "state": "InvalidPatchValue"
}
```

```json
{
  "error_code": 400,
  "message": "Cannot perform action 'CANCELLED' in state other than 'AT_PICKUP' | Current state: 'IN_DELIVERY'!!",
  "state": "DeliveryNoteActionForbidden"
}
```

**Code** : `409 Conflict`

There was an internal error. <br>
It is recommended to retry the request. <br>
If it still fails, please contact support@reebuild.com with the payload, so we can fix this as soon as possible. <br>

**Code** : `500 Internal Server Error`

There was an unexpected error. Please contact support@reebuild.com with the payload, so we can fix this as soon as possible.
