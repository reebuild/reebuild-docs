# Lieferschein

Dieser Endpoint dient zum Erstellen von digitalen Lieferscheinen. Die folgende Dokumentation beschreibt die Datenfelder
und gibt Beispiele zur Anwendung.

**URL** : `https://api.reebuild.com/industry/customer_connection/delivery_note` <br>
**Method** : `POST`

## Headers

Die folgenden Header müssen im HTTP-Request gesetzt sein: <br>

**Content-Type** : `application/json` <br>
**Api-Key¹** : `<api-key>`

¹ Der API-Key wird Ihnen im Zuge des OnBoardings per Mail zugesendet.

## Payload

Der Payload muss als [JSON](https://en.wikipedia.org/wiki/JSON)-Datei gesendet werden.

### Lieferschein

| Variable              | Beschreibung                                                                                                                                                                                                                                                                                                                                                                                                                                                                       | Datentyp | Pflichtangabe |
|:----------------------|:-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|:--------:|:-------------:|
| debug                 | Diese Variable ermöglicht ein kostenloses Testen der Anbindung <br>*Wenn sie auf "True" gesetzt ist, werden gesendete Daten gespeichert, aber in unseren Systemen nicht weiter verarbeitet. In diesem Fall wird kein digitaler Lieferschein erstellt, es kann lediglich die Funktion der API getestet werden.*                                                                                                                                                                     |   Bool   |     Nein      |
| delivery_date         | Voraussichtlicher Liefertermin <br>*Datenformat nach ISO-8601/RFC-3339 ohne Zeitzone: "%Y-%m-%d %H:%M:%S" (z.B. 2020-08-01 01:30:20) oder "%Y-%m-%dT%H:%M:%S" (z.B. 2020-08-01T01:30:20). Zeitstempel mit Zeitzone (z.B. +02:00) werden nicht akzeptiert, um eine richtige Anzeige zu garantieren.*                                                                                                                                                                                | Datetime |      Ja       |
| creator_sales_order   | Name oder Kürzel der Ersteller:in des Verkaufsauftrags <br>*Ersteller der sales_order_id*                                                                                                                                                                                                                                                                                                                                                                                          |  String  |     Nein      |
| creator_delivery_note | Name oder Kürzel der Ersteller:in des Lieferscheins <br>*Ersteller der delivery_note_id*                                                                                                                                                                                                                                                                                                                                                                                           |  String  |     Nein      |
| customer_purchase_id  | Bestellnummer des Kunden                                                                                                                                                                                                                                                                                                                                                                                                                                                           |  String  |     Nein      |
| delivery_note_id      | Lieferscheinnummer                                                                                                                                                                                                                                                                                                                                                                                                                                                                 |  String  |      Ja       |
| load_order_id         | Ladeauftragsnummer                                                                                                                                                                                                                                                                                                                                                                                                                                                                 |  String  |      Ja       |
| sales_order_id        | Verkaufsauftragsnummer des Lieferscheins                                                                                                                                                                                                                                                                                                                                                                                                                                           |  String  |      Ja       |
| cost_center_id        | Kostenstelle oder Projektnummer des Kunden                                                                                                                                                                                                                                                                                                                                                                                                                                         |  String  |     Nein      |
| license_plate_truck   | Kennzeichen des LKWs                                                                                                                                                                                                                                                                                                                                                                                                                                                               |  String  |     Nein      |
| license_plate_trailer | Kennzeichen des Anhängers                                                                                                                                                                                                                                                                                                                                                                                                                                                          |  String  |     Nein      |
| driver_name           | Name des Fahrers                                                                                                                                                                                                                                                                                                                                                                                                                                                                   |  String  |     Nein      |
| creation_date         | Erstellzeitpunkt des Lieferscheins <br/> *Datenformat nach ISO-8601/RFC-3339 ohne Zeitzone: "%Y-%m-%d %H:%M:%S" (z.B. 2020-08-01 01:30:20) oder "%Y-%m-%dT%H:%M:%S" (z.B. 2020-08-01T01:30:20). Zeitstempel mit Zeitzone (z.B. +02:00) werden nicht akzeptiert, um eine richtige Anzeige zu garantieren.*                                                                                                                                                                          | Datetime |      Ja       |
| cargo_item_amount     | Menge an Colli (Frachtstücke) <br/> *Diese Variable muss größer Nullsein.*                                                                                                                                                                                                                                                                                                                                                                                                         | Integer  |     Nein      |
| text_prefix           | Freitext zwischen Adresszeile und Produktliste                                                                                                                                                                                                                                                                                                                                                                                                                                     |  String  |     Nein      |
| text_suffix           | Freitext zwischen Produktliste und Fußzeile                                                                                                                                                                                                                                                                                                                                                                                                                                        |  String  |     Nein      |
| weight_total          | Summiertes Gesamtgewicht der Produkte <br/> *Diese Variable muss größer Nullsein.*                                                                                                                                                                                                                                                                                                                                                                                                 |  Float   |      Ja       |
| weight_unit           | Gewichtseinheit des Gesamtgewichts                                                                                                                                                                                                                                                                                                                                                                                                                                                 |  String  |      Ja       |
| customer              | Daten des Kunden <br/> *Weitere Informationen finden Sie in der nachfolgenden Tabelle unter **Customer**.*                                                                                                                                                                                                                                                                                                                                                                         |  Object  |      Ja       |
| invoice_address       | Daten der Rechnungsadresse <br/> *Weitere Informationen finden Sie in der nachfolgenden Tabelle unter **Address**.*                                                                                                                                                                                                                                                                                                                                                                |  Object  |      Ja       | 
| delivery_address      | Daten der Lieferadresse <br/> *Weitere Informationen finden Sie in der nachfolgenden Tabelle unter **Address**.*                                                                                                                                                                                                                                                                                                                                                                   |  Object  |      Ja       |
| sender_address        | Daten des Absenderadresse <br/> *Weitere Informationen finden Sie in der nachfolgenden Tabelle unter **Address**.*                                                                                                                                                                                                                                                                                                                                                                 |  Object  |      Ja       |
| purchaser             | Daten der bestellenden Person <br/> *Weitere Informationen finden Sie in der nachfolgenden Tabelle unter **Person**.*                                                                                                                                                                                                                                                                                                                                                              |  Object  |     Nein      |
| receiver              | Daten der empfangenden Person <br/> *Nach der Lieferung wird der Lieferschein automatisch an diese E-Mailadresse übermittelt. <br>Weitere Informationen finden Sie in der nachfolgenden Tabelle unter **Person**.*                                                                                                                                                                                                                                                                 |  Object  |      Ja       |
| products              | Liste der Produkte des Lieferscheins <br/>*- Die Reihenfolge der Produkte wird beibehalten. <br/>- Es ist möglich, ein Produkt mit der gleichen Artikelnummer mehrmals zu verwenden. <br/>- Es gibt einen Validierungsfehler, wenn die Produkte mit der gleichen Artikelnummer unterschiedliche Einheiten haben. <br/>- Es wird ein Validierungsfehler auftreten, wenn der Betrag <= 0 ist. <br/>Weitere Informationen finden Sie in der nachfolgenden Tabelle unter **Product**.* |  Object  |      Ja       |

### Customer

| Variable    | Beschreibung                                     | Datentyp | Pflichtangabe |
|:------------|:-------------------------------------------------|:--------:|:-------------:|
| customer_id | Ihre interne Kundenidentifikation (Kundennummer) |  String  |      Ja       |
| tax_uid     | Steuernummer bzw. UID-Nummer des Kunden          |  String  |     Nein      |
| name_prefix | Vorangestellter Textzusatz zu Kundennamen        |  String  |     Nein      |
| name        | Name des Kundenunternehmens                      |  String  |      Ja       |
| name_suffix | Nachgestellter Textzusatz zu Kundennamen         |  String  |     Nein      |

### Address

| Variable        | Beschreibung                 | Datentyp | Pflichtangabe |
|:----------------|:-----------------------------|:--------:|:-------------:|
| address_prefix  | Vorangestellter Adresszusatz |  String  |     Nein      |
| street          | Straße des Objekts           |  String  |      Ja       |
| house_nr        | Hausnummer des Objekts       |  String  |      Ja       |
| zip             | Postleitzahl des Objekts     |  String  |      Ja       |
| city            | Stadt des Objekts            |  String  |      Ja       |
| country         | Land des Objekts             |  String  |      Ja       |
| additional_info | Ergänzender Text zum Objekt  |  String  |     Nein      |

### Person

| Variable       | Beschreibung              | Datentyp |          Pflichtangabe           |
|:---------------|:--------------------------|:--------:|:--------------------------------:|
| name_prefix    | Vorangestellte Titel      |  String  |               Nein               |
| first_name     | Vorname der Person        |  String  |               Nein               |
| last_name      | Nachname der Person       |  String  |                Ja                |
| name_suffix    | Nachgestellte Titel       |  String  |               Nein               |
| mail           | E-Mail-Adresse der Person |  String  |                Ja                |
| phone_landline | Festnetznummer der Person |  String  | phone_landline oder phone_mobile |
| phone_mobile   | Handynummer der Person    |  String  | phone_landline oder phone_mobile |

### Product

| Variable     | Beschreibung                                                     | Datentyp | Pflichtangabe |
|:-------------|:-----------------------------------------------------------------|:--------:|:-------------:|
| amount       | Menge des Produkts <br/> *Diese Variable muss größer Null sein.* |  Float   |      Ja       |
| unit         | Maßeinheit des Produkts                                          |  String  |      Ja       |
| article_id   | Artikelnummer des Produkts                                       |  String  |      Ja       |
| article_name | Name des Produkts                                                |  String  |      Ja       |

### Beispiel Request Payload

```json
{
  "delivery_date": "2022-07-20 17:48:32.179951",
  "creator_sales_order": "Herbert Maurer",
  "creator_delivery_note": "Alina Berger",
  "customer_purchase_id": "326.890",
  "delivery_note_id": "LS22/564123",
  "load_order_id": "LA22/106435",
  "sales_order_id": "A22/405363",
  "cost_center_id": "221",
  "license_plate_truck": "W-28428M",
  "license_plate_trailer": "W-49058C",
  "driver_name": "Christian Bauer",
  "creation_date": "2022-06-20 17:45:00.00000",
  "cargo_item_amount": "11",
  "text_prefix": "Material laut Angebot Nr. 1238921",
  "text_suffix": "Vielen Dank für Ihre Bestellung",
  "weight_total": "1.5",
  "weight_unit": "To",
  "customer": {
    "customer_id": "256879",
    "tax_uid": "ATU 564 489 87",
    "name_prefix": "Informationen",
    "name": "Name der Firma GmbH",
    "name_suffix": "Abteilung XY"
  },
  "invoice_address": {
    "address_prefix": "",
    "street": "Rechnungsadresse",
    "house_nr": "123",
    "zip": "1130",
    "city": "Wien",
    "country": "Oesterreich",
    "additional_info": "Stock 7"
  },
  "delivery_address": {
    "address_prefix": "Kaffee an der Ecke",
    "street": "Lieferadresse",
    "house_nr": "66",
    "zip": "1100",
    "city": "Wien",
    "country": "Oesterreich",
    "additional_info": "Bitte zum Hintereingang kommen"
  },
  "sender_address": {
    "address_prefix": "",
    "street": "Absenderadresse",
    "house_nr": "12",
    "zip": "1160",
    "city": "Vienna",
    "country": "Austria",
    "additional_info": ""
  },
  "purchaser": {
    "name_prefix": "",
    "first_name": "Gregovic",
    "last_name": "Haubenbrenner",
    "name_suffix": "MSc",
    "mail": "gregovic.haubenbrenner@company.com",
    "phone_landline": "01 445 9999",
    "phone_mobile": "+43 664 445 9999"
  },
  "receiver": {
    "name_prefix": "Ing.",
    "first_name": "Roman",
    "last_name": "Bauer",
    "name_suffix": "",
    "mail": "roman.bauer@company.com",
    "phone_landline": "01 555 9999",
    "phone_mobile": "+43 676 458 9324"
  },
  "products": [
    {
      "amount": "2",
      "unit": "STK",
      "article_id": "6987324",
      "article_name": "Produkt XY groeße 3"
    },
    {
      "amount": "1",
      "unit": "STK",
      "article_id": "6987323",
      "article_name": "Produkt XY groeße 2"
    },
    {
      "amount": "500.5",
      "unit": "KG",
      "article_id": "6946722",
      "article_name": "Produkt YX"
    },
    {
      "amount": "0.75",
      "unit": "m3",
      "article_id": "A812301",
      "article_name": "Produkt 4"
    }
  ]
}
```

## Responses

**Code** : `201 CREATED`

Bei erfolgreicher Anfrage wird der HTTP-Code 201 retourniert.

**Beispiel Payload**

```json
{
  "response_code": 201
}
```

**Code** : `400 BAD REQUEST`

Die Struktur der gesendeten Daten ist korrekt, allerdings ist der Prozess wegen einem Validierungsfehler fehlgeschlagen.

**Beispiel Payload**

```json
{
    "code": 400,
    "errors": "One and the same article is described more than once with different units of measurements! Please use the same unit of measurement!",
    "status": "InvalidOperation"
}
```

**Code** : `409 Conflict`

Es ist ein interner Fehler aufgetreten.
Es wird empfohlen den Vorgang erneut durchzuführen.
Bitte kontaktieren Sie support@reebuild.com und übermitteln Sie den Payload, damit wir das Problem so schnell wie
möglich beheben können.

**Code** : `422 UNPROCESSABLE ENTITY`

Wenn gesendete Daten unvollständig oder fehlerhaft sind, wird der HTTP-Code 422 retourniert.
In der Antwort wird angegeben, welche Felder in der JSON-Datei betroffen sind.
Verschachtelte Elemente werden eingerückt retourniert.

**Beispiel Payload**

```json
{
    "code": 422,
    "errors": {
        "json": {
            "delivery_address": {
                "city": [
                    "Missing data for required field."
                ]
            },
            "delivery_note_id": [
                "Missing data for required field."
            ],
            "products": {
                "1": {
                    "article_id": [
                        "Missing data for required field."
                    ],
                    "article_name": [
                        "Missing data for required field."
                    ]
                }
            }
        }
    },
    "status": "Unprocessable Entity"
}
```

**Code** : `500 Internal Server Error`

Es ist ein unerwarteter Fehler aufgetreten. Bitte kontaktieren Sie support@reebuild.com und übermitteln Sie den
Payload, damit wir das
Problem so schnell wie möglich beheben können.
