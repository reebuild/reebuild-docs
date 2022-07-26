# Lieferschein Pdf

Dieser Endpoint dient zum Abholen von digitalen Lieferscheinen in PDF Form. 

**URL** : `https://api.reebuild.com/industry/customer_connection/delivery_note/<deliveryNoteId>/pdf` 

**Method** : `GET`

## Header

Die folgenden Header müssen im HTTP-Request gesetzt sein: <br>

**Content-Type** : `application/pdf`

**Api-Key¹** : `<api-key>`

¹ Der API-Key wird Ihnen im Zuge des OnBoardings per Mail zugesendet.

## Url Parameter

Der `deliveryNoteId` Abschnitt der Url wird dazu benutzt, um Ihren Lieferschein zu identifizieren. <br>
Beim Einsetzen dieses Wertes, entfernen Sie bitte die spitzen Klammern.

## Beispiel

**URL** : `https://api.reebuild.com/industry/customer_connection/delivery_note/LS2635G9/pdf` <br>

## Responses

**Code** : `200 Ok`

Bei erfolgreicher Anfrage mit Weiterleitung wird der HTTP-Code `200` retourniert. <br>
Je nach verwendetem Client und dessen Konfiguration, können Sie automatisch auf den PDF-Download weitergeleitet werden. <br>
Bei erfolgreicher Weiterleitung, befindet sich das PDF in der Antwort des Servers. <br>

**Code** : `302 Found`

Bei erfolgreicher Anfrage ohne Weiterleitung wird der HTTP-Code `302` retourniert. <br>
Je nach verwendetem Client und dessen Konfiguration, können Sie automatisch auf den PDF-Download weitergeleitet werden. <br>
Bei keiner Weiterleitung, steht die Url für den Download im 'location' Header. <br>


**Code** : `409 Conflict`

Es ist ein interner Fehler aufgetreten. <br>
Es wird empfohlen den Vorgang erneut durchzuführen. <br>
Bitte kontaktieren Sie support@reebuild.com und übermitteln Sie den Payload, damit wir das Problem so schnell wie <br>
möglich beheben können.


**Code** : `500 Internal Server Error`

Es ist ein unerwarteter Fehler aufgetreten. Bitte kontaktieren Sie support@reebuild.com und übermitteln Sie den <br>
Payload, damit wir das Problem so schnell wie möglich beheben können.
