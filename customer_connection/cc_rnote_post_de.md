# Return Delivery Note

Sends the return delivery note data to the server.
If the validation fails, a descriptive error will be returned.
Will be saved otherwise and returns the created pk.

This is only possible if a delivery note was previously created on our system. 
Else the error [Delivery note mismatch](#delivery-note-mismatch) will be thrown.

**URL** : `/customer_service/return_delivery_note`

**Method** : `POST`

## Headers

In order for the request to work the following header is necessary: <br>

**Content-Type** : `application/json`

## Payload

The payload is a json in the body containing following properties:

**Payload example**

| Property                    | Description                                                                                                                                                                                                                                 | Datatype | Mandatory |
|:----------------------------|:--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|:--------:|:---------:|
| debug                       | This flag is used for development. If it is 'True' the data sent will be persisted, but not sent to other systems. That way you can still test other endpoint functionalities.                                                              |   Bool   |     N     |
| delivery_date               | The naive datetime when the delivery is expected. The format is localized "%Y-%m-%d %H:%M:%S". This will be displayed on the delivery note pdf. If a timezone is given (e.g. +02:00) an error will be thrown in order to prevent confusion. | Datetime |     Y     |
| creator                     | The creator of the delivery note.                                                                                                                                                                                                           |  String  |     Y     |
| editor                      | The editor of the delivery note.                                                                                                                                                                                                            |  String  |     Y     |
| order_id                    | The identification of the order you made in your system.                                                                                                                                                                                    |  String  |     N     |
| return_delivery_note_id     | The identification of the return delivery note in your system.                                                                                                                                                                              |  String  |     Y     |
| reference_delivery_note_id  | The identification of the referenced delivery note in your system.                                                                                                                                                                          |  String  |     Y     |
| load_order_id               | The identification of the order/job to load the truck.                                                                                                                                                                                      |  String  |     N     |
| job_id                      | The job number of the delivery note.                                                                                                                                                                                                        |  String  |     Y     |
| cost_center_id              | The cost centre or project id of the customer.                                                                                                                                                                                              |  String  |     Y     |
| creation_place              | The creation place of the delivery note.                                                                                                                                                                                                    |  String  |     Y     |
| creation_date               | The naive creation datetime of the delivery note with format localized "%Y-%m-%d %H:%M:%S". This will be displayed on the delivery note pdf. If a timezone is given (e.g. +02:00) an error will be thrown in order to prevent confusion.    | Datetime |     Y     |
| colli_amount                | The amount of collis in the delivery. Must be a positive number.                                                                                                                                                                            | Integer  |     Y     |
| text_entry_product_prefix   | Some text you want to insert above the product listing.                                                                                                                                                                                     |  String  |     N     |
| weight_total                | The total weight of the products. Must be a positive number.                                                                                                                                                                                |  Float   |     Y     |
| weight_unit                 | The weight unit of the total weight.                                                                                                                                                                                                        |  String  |     Y     |
| text_entry_end              | Some text you want to insert beneath the product listing.                                                                                                                                                                                   |  String  |     N     |
| customer                    | The data about the customer. For further information see its own table documentation below. [Customer Object](#customer-object)                                                                                                             |  Object  |     Y     |
| invoice_address             | The data about the invoice address. For further information see its own table documentation below - column "Restricted". [R-Address Object](#address-object)                                                                                |  Object  |     Y     |
| delivery_address            | The data about the delivery address. For further information see its own table documentation below - column "Restricted". [R-Address Object](#address-object)                                                                               |  Object  |     Y     |
| sender_address              | The data about the sender location. For further information see its own table documentation below - column "Unrestricted". [U-Address Object](#address-object)                                                                              |  Object  |     Y     |
| contact_person_customer     | The data about one of two contact persons. For further information see its own table documentation below. [Contact Person Object](#contact-person-object)                                                                                   |  Object  |     N     |
| contact_person_construction | The data about one of two contact persons. For further information see its own table documentation below. [Contact Person Object](#contact-person-object)                                                                                   |  Object  |     N     |
| products                    | The not empty list of products of the delivery note. For further information see its own table documentation below. [Product List Object](#product-list-object)                                                                             |  Object  |     Y     |

### Customer Object

| Property    | Description                      | Datatype | Mandatory |
|:------------|:---------------------------------|:--------:|:---------:|
| customer_id | Your intern customer identifier. |  String  |     N     |
| tax_uid     | Identifier of the tax number.    |  String  |     Y     |
| name_prefix | Text above the customer name.    |  String  |     N     |
| name        | The name of the customer.        |  String  |     Y     |
| name_suffix | Text beneath the customer name.  |  String  |     N     |

### Address Object

| Property       | Description                                                        | Datatype | Mandatory <br/> Restricted | Mandatory </br> Unrestricted |
|:---------------|:-------------------------------------------------------------------|:--------:|:--------------------------:|:----------------------------:|
| address_prefix | Text above the address.                                            |  String  |             N              |              N               |
| street         | The delivery street.                                               |  String  |             Y              |              N               |
| house_nr       | The delivery house_nr.                                             |  String  |             Y              |              N               |
| zip            | The post code of the delivery address.                             |  String  |             Y              |              N               |
| city           | The city of the delivery address.                                  |  String  |             Y              |              Y               |
| supplement     | The additional or complementary text beneath the delivery address. |  String  |             N              |              N               |

### Contact Person Object

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

### Product List Object

The order of the products will be persisted. <br>
It is possible to pass a product with the same article_number several times. <br>
There will be a validation error if the products with the same article_number have different units. <br>
There will be a validation error if the amount is <= 0. <br>

| Property            | Description                                           | Datatype | Mandatory |
|:--------------------|:------------------------------------------------------|:--------:|:---------:|
| amount              | The amount of the product. Must be a positive number. |  Float   |     Y     |
| unit                | The unit of the product.                              |  String  |     Y     |
| article_number      | The article number of the product.                    |  String  |     Y     |
| article_description | The description of the product.                       |  String  |     Y     |

**Payload example without description**

```json
{
  "reference_delivery_note_id": "Lieferscheinnummer 125",
  "return_delivery_note_id": "return Lieferscheinnummer 123",
  "delivery_date": "2022-07-20 17:48:32.179951",
  "creator": "a. k.",
  "editor": "c. m.",
  "customer": {
    "tax_uid": "U1222RH",
    "name": "Max schoebl GmbH"
  },
  "invoice_address": {
    "street": "Invoice address",
    "house_nr": "123",
    "zip": "1130",
    "city": "Vienna"
  },
  "delivery_address": {
    "street": "Delivery address",
    "house_nr": "123",
    "zip": "1100",
    "city": "Vienna"
  },
  "sender_address": {
    "city": "Vienna"
  },
  "cost_center_id": "PN7231G6",
  "job_id": "A22305/63-0003",
  "creation_place": "Vienna 1170",
  "creation_date": "2022-06-20T17:45:00.00000",
  "colli_amount": "11",
  "products": [
    {
      "amount": "1",
      "unit": "STK",
      "article_number": "A341234U2",
      "article_description": "Fensterglas groeße 3"
    }
  ],
  "weight_total": "50",
  "weight_unit": "kg"
}
```

## Success Response

**Code** : `201 CREATED`

The terminology pk stands for primary key and was chosen to distinguish the customer given 'ids' and the internal 'pks'
for serverside items.
If the request was valid there will be a response json with the pk of the saved return delivery note.
The field named 'pk' might be needed for further requests.

**Content examples**

```json
{
  "content": {
    "pk": 19
  },
  "response_code": 201
}
```

## Failure Response

**Code** : '400 Bad Request'

### Validation Error

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

### Delivery note mismatch

```json
{
  "error_code": 400,
  "messages": "No matching 'delivery_note' with pk: 'not_existing_note'!"
}
```

### Cost center mismatch

```json
{
  "error_code": 400,
  "messages": "Given cost center does not match! Given cost center was '98765Example' but '56789Example' was expected!"
}
```

### Product mismatch

```json
{
  "error_code": 400,
  "messages": "No matching product ' <DReturnProduct>: { amount: 2.0, unit: STK, article_number: A341234U2not same }' found on orig delivery note with id: '123ExampleID'!"
}
```

### Customer mismatch

```json
{
  "error_code": 400,
  "messages": "Given customer id does not match! Given customer id was 'c7bea9c92b56-8f28-a784-e770-81a0cf5c' but 'c5fc0a18-077e-487a-82f8-65b29c9aeb7c' was expected!"
}
```

### Unit mismatch

```json
{
  "error_code": 400,
  "messages": "Given unit of measurement does not match! Given unit of measurement was 'USD' but 'EUR' was expected!"
}
```

### Amount mismatch

```json
{
  "error_code": 400,
  "messages": "It is not possible to return a bigger amount of wares than received! Given amount was 847.0 but a maximum of 837.0 was expected!"
}
```

**Code** : '409 Conflict'

There was an error with the intern mapping. Please contact support@reebuild.com with the payload, so we can fix this
asap.

**Code** : '500 Internal Server Error'

There was an unexpected error. Please contact support@reebuild.com with the payload, so we can fix this asap. 
