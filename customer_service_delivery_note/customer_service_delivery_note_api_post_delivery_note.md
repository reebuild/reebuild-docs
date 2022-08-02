# Save Delivery Note

Send the delivery note data to the server and save it.

**URL** : `/delivery_note`

**Method** : `POST`

## Headers

In order for the request to work the following header is necessary: <br>

**Content-Type** : `application/json`

## Payload

The payload is a json in the body containing following properties:

**Payload example**

| Property                    | Description                                                                                                                                                                              | Datatype | Mandatory |
|:----------------------------|:-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|:--------:|:---------:|
| debug                       | This flag is used for development. If it is 'True' the data sent will be persisted, but not sent to other systems. That way you can still test the deletion of a delivery_note endpoint. |   Bool   |     N     |
| delivery_date               | The date when the delivery is expected. The format is "YYYY-MM-DD HH:MM:SS".                                                                                                             | Datetime |     Y     |
| creator                     | The creator of the delivery note                                                                                                                                                         |  String  |     Y     |
| editor                      | The editor of the delivery note                                                                                                                                                          |  String  |     Y     |
| order_id                    | The identification of the order you made in your system.                                                                                                                                 |  String  |     Y     |
| delivery_note_id            | The identification of the delivery note in your system.                                                                                                                                  |  String  |     Y     |
| load_order_id               | The identification of the order/job to load the truck.                                                                                                                                   |  String  |     Y     |
| job_id                      | The job number of the delivery note.                                                                                                                                                     |  String  |     Y     |
| cost_center_id              | The cost centre or project id of the customer.                                                                                                                                           |  String  |     Y     |
| delivery_method             | The delivery method.                                                                                                                                                                     |  String  |     Y     |
| creation_place              | The creation place of the delivery note.                                                                                                                                                 |  String  |     Y     |
| creation_date               | The creation date of the delivery note with format "YYYY-MM-DD HH:MM:SS".                                                                                                                | Datetime |     Y     |
| colli_amount                | The amount of collis in the delivery.                                                                                                                                                    | Integer  |     Y     |
| text_entry_product_prefix   | Some text you want to insert above the product listing.                                                                                                                                  |  String  |     N     |
| weight_total                | The total weight of the products.                                                                                                                                                        |  Float   |     Y     |
| weight_unit                 | The weight unit of the total weight.                                                                                                                                                     |  String  |     Y     |
| text_entry_end              | Some text you want to insert beneath the product listing.                                                                                                                                |  String  |     N     |
| customer                    | The data about the customer. For further information see its own table documentation below. [Customer Object](#customer-object)                                                          |  Object  |     Y     |
| invoice_address             | The data about the invoice address. For further information see its own table documentation below - column "Restricted". [R-Address Object](#address-object)                             |  Object  |     Y     |
| delivery_address            | The data about the delivery address. For further information see its own table documentation below - column "Restricted". [R-Address Object](#address-object)                            |  Object  |     Y     |
| sender_address              | The data about the sender location. For further information see its own table documentation below - column "Unrestricted". [U-Address Object](#address-object)                           |  Object  |     Y     |
| contact_person_customer     | The data about one of two contact persons. For further information see its own table documentation below. [Contact Person Object](#contact-person-object)                                |  Object  |     Y     |
| contact_person_construction | The data about one of two contact persons. For further information see its own table documentation below. [Contact Person Object](#contact-person-object)                                |  Object  |     N     |
| products                    | The not empty list of products of the delivery note. For further information see its own table documentation below. [Product List Object](#product-list-object)                          |  Object  |     Y     |

<h3 id="customer-object">Customer Object</h3>

| Property    | Description                                        | Datatype | Mandatory |
|:------------|:---------------------------------------------------|:--------:|:---------:|
| identifier  | Custom identifier of the customer by your company. |  String  |     Y     |
| tax_uid     | Identifier of the tax number.                      |  String  |     Y     |
| name_prefix | Text above the customer name.                      |  String  |     N     |
| name        | The name of the customer.                          |  String  |     Y     |
| name_suffix | Text beneath the customer name.                    |  String  |     N     |

<h3 id="address-object">Address Object</h3>

| Property       | Description                                                        | Datatype | Mandatory <br/> Restricted | Mandatory </br> Unrestricted |
|:---------------|:-------------------------------------------------------------------|:--------:|:--------------------------:|:----------------------------:|
| address_prefix | Text above the address.                                            |  String  |             N              |              N               |
| street         | The delivery street.                                               |  String  |             Y              |              N               |
| house_nr       | The delivery house_nr.                                             |  String  |             Y              |              N               |
| zip            | The post code of the delivery address.                             |  String  |             Y              |              N               |
| city           | The city of the delivery address.                                  |  String  |             Y              |              Y               |
| supplement     | The additional or complementary text beneath the delivery address. |  String  |             N              |              N               |

<h3 id="contact-person-object">Contact Person Object</h3>

| Property       | Description                              | Datatype |           Mandatory            |
|:---------------|:-----------------------------------------|:--------:|:------------------------------:|
| name_prefix    | The prefix of the persons name.          |  String  |               N                |
| first_name     | The first name of the person.            |  String  |               Y                |
| last_name      | The last name of the person.             |  String  |               Y                |
| name_suffix    | The suffix of the persons name.          |  String  |               N                |
| fax            | The fax of the person.                   |  String  |               N                |
| mail           | The mail of the person.                  |  String  |               Y                |
| phone_landline | The landline phone number of the person. |  String  | phone_landline or phone_mobile |
| phone_mobile   | The mobile phone number of the person.   |  String  | phone_landline or phone_mobile |

<h3 id="product-list-object">Product List Object</h3>

| Property            | Description                        | Datatype | Mandatory |
|:--------------------|:-----------------------------------|:--------:|:---------:|
| amount              | The amount of the product.         |  Float   |     Y     |
| unit                | The unit of the product.           |  String  |     Y     |
| article_number      | The article number of the product. |  String  |     Y     |
| article_description | The description of the product.    |  String  |     Y     |

**Payload example without description**

```json
{
  "delivery_date": "2022-07-20 17:48:32.179951",
  "creator": "a. k.",
  "editor": "c. m.",
  "customer": {
    "identifier": "test",
    "tax_uid": "U1222RH",
    "name_prefix": "Buy clever",
    "name": "Max schoebl GmbH",
    "name_suffix": "Vienna"
  },
  "invoice_address": {
    "address_prefix": "Billa",
    "street": "Invoice address",
    "house_nr": "123",
    "zip": "1130",
    "city": "Vienna",
    "supplement": "Floor 7"
  },
  "delivery_address": {
    "address_prefix": "Merkur",
    "street": "Delivery address",
    "house_nr": "123",
    "zip": "1100",
    "city": "Vienna",
    "supplement": "Behind Supermarket"
  },
  "sender_address": {
    "city": "Vienna"
  },
  "order_id": "Bestellnummer 3",
  "delivery_note_id": "Lieferscheinnummer 123",
  "load_order_id": "Ladeauftragnummer U235",
  "cost_center_id": "PN7231G6",
  "job_id": "A22305/63-0003",
  "contact_person_customer": {
    "name_prefix": "",
    "first_name": "Gregovic",
    "last_name": "Haubenbrenner",
    "name_suffix": "Master",
    "fax": "7818736218736",
    "mail": "gregovic.haubenbrenner@company.com",
    "phone_landline": "01 445 9999",
    "phone_mobile": "01 445 9999"
  },
  "contact_person_construction": {
    "name_prefix": "Slave",
    "first_name": "Roman",
    "last_name": "Bauer",
    "name_suffix": "",
    "fax": "123135431",
    "mail": "roman.bauer@company.com",
    "phone_landline": "01 555 9999",
    "phone_mobile": "01 555 9999"
  },
  "delivery_method": "M",
  "creation_place": "Vienna 1170",
  "creation_date": "2022-06-20T17:45:00.00000",
  "colli_amount": "11",
  "text_entry_product_prefix": "MATERIAL LAUT AUFSTELLUNG",
  "products": [
    {
      "amount": "2",
      "unit": "STK",
      "article_number": "A341234U2",
      "article_description": "Fensterglas groeße 3"
    },
    {
      "amount": "1",
      "unit": "STK",
      "article_number": "A38522344U2",
      "article_description": "Fensterglas groeße 2"
    },
    {
      "amount": "500.5",
      "unit": "KG",
      "article_number": "A3A76ZU2",
      "article_description": "Fluessigbeton"
    },
    {
      "amount": "837.3",
      "unit": "EUR",
      "article_number": "A812301",
      "article_description": "Pizza"
    }
  ],
  "weight_total": "50.0",
  "weight_unit": "kg",
  "text_entry_end": " ENDE "
}
```

## Success Response

**Code** : `200 OK`

If the request was valid there will be a response json with the saved data.
There will also be a field named 'id' which you will need for further requests like updating the state of a delivery
note.

**Content examples**

```json
{
  "id": 1234,
  "...": "copy of the payload json which the server receives"
}
```

## Failure Response

**Code** : '400 Bad Request'

If our validation determines that there are missing fields there will be a 400 response like the following.
The response will indicate what fields are missing in the json.
All missing nested fields will be printed in a separate nested lines..

**Content examples**

```json
{
  "error_code": 400,
  "messages": {
    "contact_person_construction": [
      "Missing data for required field."
    ],
    "delivery_date": [
      "Not a valid datetime."
    ],
    "invoice_address": {
      "house_nr": [
        "Missing data for required field."
      ],
      "street": [
        "Missing data for required field."
      ],
      "zip": [
        "Missing data for required field."
      ]
    },
    "job_id": [
      "Missing data for required field."
    ],
    "products": {
      "0": {
        "amount": [
          "Not a valid number."
        ]
      }
    },
    "weight_total": [
      "Not a valid number."
    ]
  }
}
```

**Code** : '409 Conflict'

There was an error with the intern mapping. Please contact support@reebuild.com with the payload, so we can fix this asap. 

**Code** : '500 Internal Server Error'

There was an unexpected error. Please contact support@reebuild.com with the payload, so we can fix this asap. 
