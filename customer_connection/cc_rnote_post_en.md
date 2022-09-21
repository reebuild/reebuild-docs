# Return Delivery Note

This endpoint is used to create digital return delivery notes. The following documentation describes the data fields and
gives examples.

**URL** : `https://api.reebuild.com/industry/customer_connection/return_delivery_note` <br>
**Method** : `POST`

## Headers

In order for the request to work the following headers are necessary: <br>

**Content-Type** : `application/json`<br>
**Api-Key¹** : `<api-key>`

¹ You receive the API-Key in the course of the OnBoarding by mail.

## Payload

The payload is a [JSON](https://en.wikipedia.org/wiki/JSON) in the body containing following properties:

### Return Delivery Note

| Property                     | Description                                                                                                                                                                                                                                                                                                                                                                                                     | Datatype | Mandatory |
|:-----------------------------|:----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|:--------:|:---------:|
| debug                        | This flag allows free testing of the connection <br>*If it's "True", sent data will be saved but not processed further in our systems. In this case, no digital delivery note is created, only the function of the API can be tested. The flag is set to "True" automatically if the provided API-Key has the role "Debug".*                                                                                                                                                                         |   Bool   |    No     |
| delivery_date                | Naive datetime of expected return delivery <br>*Data format according to ISO-8601/RFC-3339 without time zone: "%Y-%m-%d %H:%M:%S" (e.g. 2020-08-01 01:30:20) or "%Y-%m-%dT%H:%M:%S" (z.B. 2020-08-01T01:30:20). If a timezone is given (e.g. +02:00) an error will be thrown in order to guarantee a correct display.*                                                                                          | Datetime |    Yes    |
| creator_return_order         | Name or initials of the author of the return order <br>*Creator of return_order_id*                                                                                                                                                                                                                                                                                                                             |  String  |    No     |
| creator_return_delivery_note | Name or initials of the author of the return delivery note  <br>*Creator of return_delivery_note_id*                                                                                                                                                                                                                                                                                                            |  String  |    No     |
| customer_purchase_id         | Order number of the customer                                                                                                                                                                                                                                                                                                                                                                                    |  String  |    No     |
| return_delivery_note_id      | Identification number of the return delivery note                                                                                                                                                                                                                                                                                                                                                               |  String  |    Yes    |
| reference_sales_order_id     | Reference order <br> *Identification number of the reference sales order*                                                                                                                                                                                                                                                                                                                                       |  String  |    Yes    |
| load_order_id                | Identification number of the load order                                                                                                                                                                                                                                                                                                                                                                         |  String  |    No     |
| return_order_id              | Identification number of the return order                                                                                                                                                                                                                                                                                                                                                                       |  String  |    No     |
| cost_center_id               | Cost center or project id of the customer                                                                                                                                                                                                                                                                                                                                                                       |  String  |    No     |
| license_plate_truck          | License plate number of the truck                                                                                                                                                                                                                                                                                                                                                                               |  String  |    No     |
| license_plate_trailer        | License plate number of the trailer                                                                                                                                                                                                                                                                                                                                                                             |  String  |    No     |
| driver_name                  | Driver name                                                                                                                                                                                                                                                                                                                                                                                                     |  String  |    No     |
| creation_date                | Naive datetime of return delivery note creation <br>*Data format according to ISO-8601/RFC-3339 without time zone: "%Y-%m-%d %H:%M:%S" (e.g. 2020-08-01 01:30:20) or "%Y-%m-%dT%H:%M:%S" (z.B. 2020-08-01T01:30:20). If a timezone is given (e.g. +02: 00) an error will be thrown in order to guarantee a correct display.*                                                                                    | Datetime |    Yes    |
| cargo_item_amount            | Amount of items (colli) in the load <br>*Must be a positive number.*                                                                                                                                                                                                                                                                                                                                            | Integer  |    No     |
| text_prefix                  | Free text entry between address line and product list                                                                                                                                                                                                                                                                                                                                                           |  String  |    No     |
| text_suffix                  | Free text entry between Product list and footer                                                                                                                                                                                                                                                                                                                                                                 |  String  |    No     |
| weight_total                 | Total weight of the products <br>*Must be a positive number.*                                                                                                                                                                                                                                                                                                                                                   |  Float   |    Yes    |
| weight_unit                  | Weight unit of the total weight                                                                                                                                                                                                                                                                                                                                                                                 |  String  |    Yes    |
| customer                     | Data on the customer <br>*For further information, see the **Customer** table below.*                                                                                                                                                                                                                                                                                                                           |  Object  |    Yes    |
| invoice_address              | Data on the invoice address <br>*For further information, see the **Address** table below.*                                                                                                                                                                                                                                                                                                                     |  Object  |    Yes    |
| delivery_address             | Data of the initial delivery address ( reference order) <br>*For further information, see the **Address** table below.*                                                                                                                                                                                                                                                                                         |  Object  |    Yes    |
| sender_address               | Data on the initial sender address (reference order) <br>*For further information, see the **Address** table below.*                                                                                                                                                                                                                                                                                            |  Object  |    Yes    |
| purchaser                    | Data on the purchasing person (reference order) <br>*For further information, see the **Person** table below.*                                                                                                                                                                                                                                                                                                  |  Object  |    No     |
| receiver                     | Data on the contact person, who has received the initial delivery (reference order) <br> *After delivery, the delivery note is automatically sent to this mail address. <br>For further information, see **Person** below.*                                                                                                                                                                                     |  Object  |    Yes    |
| products                     | List of all products on the return delivery note <br>*- The order of the products is maintained. <br>- It is possible to use a product with the same item number more than once. <br>- There will be a validation error if products with the same item number have different units. <br>- There will be a validation error if the amount is <= 0.<br> For further information see the **Product** table below.* |  Object  |    Yes    |

### Customer

| Property    | Description                              | Datatype | Mandatory |
|:------------|:-----------------------------------------|:--------:|:---------:|
| customer_id | Your intern customer identifier          |  String  |    Yes    |
| tax_uid     | Tax number or VAT number of the customer |  String  |    No     |
| name_prefix | Preceding text addition to customer name |  String  |    No     |
| name        | Name of the client organization          |  String  |    Yes    |
| name_suffix | Posterior text addition to customer name |  String  |    No     |

### Address

| Property        | Description                                           | Datatype | Mandatory |
|:----------------|:------------------------------------------------------|:--------:|:---------:|
| address_prefix  | Preceding address addition                            |  String  |    No     |
| street          | Street of the entity                                  |  String  |    Yes    |
| house_nr        | House number of the entity                            |  String  |    Yes    |
| zip             | Post code of the entity                               |  String  |    Yes    |
| city            | City of the entity                                    |  String  |    Yes    |
| country         | Country of the entity                                 |  String  |    Yes    |
| additional_info | Additional or complementary information of the entity |  String  |    No     |

### Person

| Property       | Description                         | Datatype |           Mandatory            |
|:---------------|:------------------------------------|:--------:|:------------------------------:|
| name_prefix    | Preceding title                     |  String  |               No               |
| first_name     | First name of the person            |  String  |               No               |
| last_name      | Last name of the person             |  String  |              Yes               |
| name_suffix    | Posterior title                     |  String  |               No               |
| mail           | Mail of the person                  |  String  |              Yes               |
| phone_landline | Landline phone number of the person |  String  | phone_landline or phone_mobile |
| phone_mobile   | Mobile phone number of the person   |  String  | phone_landline or phone_mobile |

### Product List Object

| Property       | Description                                             | Datatype | Mandatory |
|:---------------|:--------------------------------------------------------|:--------:|:---------:|
| amount         | Amount of the product <br> *Must be a positive number.* |  Float   |    Yes    |
| unit           | Unit of the product                                     |  String  |    Yes    |
| article_id | Article number of the product                           |  String  |    Yes    |
| article_name   | Name of the product                                     |  String  |    Yes    |

### Request payload example

```json
{
  "delivery_date": "2022-07-20 17:48:32.179951",
  "creator_return_order": "Herbert Maurer",
  "creator_return_delivery_note": "Alina Berger",
  "customer_purchase_id": "326.991",
  "return_delivery_note_id": "RS22/24561",
  "reference_sales_order_id": "A22/405363",
  "load_order_id": "LA22/106435",
  "return_order_id": "A22/405466",
  "cost_center_id": "221",
  "license_plate_truck": "W-28428M",
  "license_plate_trailer": "W-49058C",
  "driver_name": "Christian Bauer",
  "creation_date": "2022-06-20 17:45:00.00000",
  "cargo_item_amount": "1",
  "text_prefix": "Return for order Nr. A22/405363",
  "text_suffix": "Thank you",
  "weight_total": "0.2",
  "weight_unit": "To",
  "customer": {
    "customer_id": "256879",
    "tax_uid": "ATU 564 489 87",
    "name_prefix": "Some infos",
    "name": "Name of the company GmbH",
    "name_suffix": "Department XY"
  },
  "invoice_address": {
    "address_prefix": "",
    "street": "Invoice address",
    "house_nr": "123",
    "zip": "1130",
    "city": "Vienna",
    "country": "Austria",
    "additional_info": "Floor 7"
  },
  "delivery_address": {
    "address_prefix": "Coffee at the Corner",
    "street": "Delivery address",
    "house_nr": "66",
    "zip": "1100",
    "city": "Vienna",
    "country": "Austria",
    "additional_info": "please come to the back entrance"
  },
  "sender_address": {
    "address_prefix": "",
    "street": "Sender address",
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
      "amount": "1",
      "unit": "STK",
      "article_id": "6987324",
      "article_name": "Produkt XY size 3"
    }
  ]
}
```

## Responses

**Code** : `201 CREATED`

If the request is successful, the HTTP code 201 is returned.

**Payload example**

```json
{
  "response_code": 201
}
```

**Code** : `400 BAD REQUEST`

The structure of the sent data is correct, but the process failed due to a validation error.

**Payload example**

```json
{
    "code": 400,
    "errors": "One and the same article is described more than once with different units of measurements! Please use the same unit of measurement!",
    "status": "InvalidOperation"
}
```

**Code** : `409 Conflict`

There was an internal error.
It is recommended to retry the request.
If it still fails, please contact support@reebuild.com with the payload, so we can fix this as soon as possible.

**Code** : `422 UNPROCESSABLE ENTITY`

If sent data is incomplete or faulty there will be a 422 response like the following.
The response will indicate what fields are missing in the json.
All missing nested fields will be printed in a separate nested lines.

**Payload example**

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
            "return_delivery_note_id": [
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

There was an unexpected error. Please contact support@reebuild.com with the payload, so we can fix this as soon as
possible. 
