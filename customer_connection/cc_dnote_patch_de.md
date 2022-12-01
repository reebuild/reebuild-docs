# Update Delivery Note

Dieser Endpunkt dient dazu Änderungen an Lieferscheinen vorzunehmen. <br>
Aktuell ist die einzige freigeschaltete Operation den Status zu verändern. <br>
Dieser kann nur auf storniert gesetzt werden, wenn gegebener Lieferschein noch nicht unterschrieben worden ist. <br>

**URL** : `https://api.reebuild.com/industry/customer_connection/delivery_note/<deliveryNoteId>`

**Method** : `PATCH`

## Headers

Die folgenden Header müssen im HTTP-Request gesetzt sein: <br>

**Content-Type** : `application/json` <br>
**Api-Key¹** : `<api-key>`

¹ Der API-Key wird Ihnen im Zuge des OnBoardings per Mail zugesendet.

## Url

Der `deliveryNoteId` Abschnitt der Url wird dazu benutzt, um Ihren fehlerhaften Lieferschein zu identifizieren. <br>
Beim Einsetzen dieses Wertes, entfernen Sie bitte die spitzen Klammern.

## Payload

Der Payload muss als [JSON](https://en.wikipedia.org/wiki/JSON)-Datei gesendet werden. <br>
Aktuell wird nur das Feld `new_state` unterstützt. <br>
Es gibt aktuell nur einen zulässigen Wert: `CANCELLED` <br>

## Beispiel

**URL** : `https://api.reebuild.com/industry/customer_connection/delivery_note/LS2649G34` <br> <br>
**Payload** :
```json
{
  "new_state": "CANCELLED"
}
```

## Success Response

**Code** : `200 OK`

Wenn die Anfrage erfolgreich durchgeführt werden konnte, werden die neu gesetzten Werte als Antwort übermittelt.

**Response example**

```json
{
  "state": "CANCELLED"
}
```

## Failure Response

**Code** : `400 Bad Request`

Wird als Antwort gesendet, wenn eine der folgenden Kriterien zutrifft:
- Es wurde ein ungültiger Wert zum Setzen an den Endpunkt übergeben
- Der Wert konnte, durch Beschränkungen, nicht gesetzt werden <br>(z.B.: Der Lieferschein ist bereits unterschrieben)

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

Es ist ein interner Fehler aufgetreten. <br>
Es wird empfohlen den Vorgang erneut durchzuführen. <br>
Bitte kontaktieren Sie support@reebuild.com und übermitteln Sie den Payload, damit wir das Problem so schnell wie <br>
möglich beheben können.

**Code** : `500 Internal Server Error`

Es ist ein unerwarteter Fehler aufgetreten. Bitte kontaktieren Sie support@reebuild.com und übermitteln Sie den <br>
Payload, damit wir das Problem so schnell wie möglich beheben können.
