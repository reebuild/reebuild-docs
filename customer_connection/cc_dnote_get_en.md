# Delivery Note

This endpoint is used to retrieve delivery notes in PDF form.

**URL** : `https://api.reebuild.com/industry/customer_connection/delivery_note` <br>
**Method** : `GET`

## Header

The following headers must be set: <br>

**Content-Type** : `application/pdf` <br>
**Api-Key¹** : `<api-key>`

¹ You receive the API-Key in the course of the OnBoarding by mail.

## Query Parameter

The following query parameters must be set: <br>

**deliveryNoteId** : `Identification of the delivery note` <br>

## Example

**URL** : `https://api.reebuild.com/industry/customer_connection/delivery_note?deliveryNoteId=LS2635G9` <br>

## Responses

**Code** : `200 Ok`

If the request is successful and redirected, the HTTP-Code `200` will be returned. <br>
Depending on the client used and its configuration, you might be automatically redirected to the PDF download. <br>
If the redirection is successful, the PDF will be in the server's response. <br>

**Code** : `302 Found`

If the request is successful and not redirected, the HTTP-Code `302` will be returned. <br>
Depending on the client used and its configuration, you might be automatically redirected to the PDF download. <br>
If there is no redirection, you can find the url for the download in the 'location' header. <br>

**Code** : `409 Conflict`

There was an internal error. <br>
It is recommended to retry the request. <br>
If it still fails, please contact support@reebuild.com with the payload, so we can fix this as soon as possible. <br>


**Code** : `500 Internal Server Error`

There was an unexpected error. Please contact support@reebuild.com with the payload, so we can fix this as soon as possible.
