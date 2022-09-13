# Delivery Note

This endpoint is used to create digital delivery notes. The following documentation describes the data fields and gives
examples.

**URL** : `https://api.reebuild.com/industry/customer_connection/delivery_note` <br>
**Method** : `POST`

## Headers

In order for the request to work the following headers are necessary: <br>

**Content-Type** : `application/json`<br>
**Api-Key¹** : `Api-Key`

¹ You receive the API-Key in the course of the OnBoarding by mail.

## Payload

The payload is a [JSON](https://en.wikipedia.org/wiki/JSON) in the body containing following properties:

### Delivery Note

| Property              | Description                                                                                                                                                                                                                                                                                                                                                                                              | Datatype | Mandatory |
|:----------------------|:---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|:--------:|:---------:|
| debug                 | This flag allows free testing of the connection <br>*If it's "True", sent data will be saved but not processed further in our systems. In this case, no digital delivery note is created, only the function of the API can be tested.*                                                                                                                                                                   |   Bool   |    No     |
| delivery_date         | Naive datetime of expected delivery <br>*Data format according to ISO-8601/RFC-3339 without time zone: "%Y-%m-%d %H:%M:%S" (e.g. 2020-08-01 01:30:20) or "%Y-%m-%dT%H:%M:%S" (z.B. 2020-08-01T01:30:20). If a timezone is given (e.g. +02:00) an error will be thrown in order to guarantee a correct display.*                                                                                          | Datetime |    Yes    |
| creator_sales_order   | Name or initials of the author of the sales order <br>*Creator of sales_order_id*                                                                                                                                                                                                                                                                                                                        |  String  |    No     |
| creator_delivery_note | Name or initials of the author of the delivery note  <br>*Creator of delivery_note_id*                                                                                                                                                                                                                                                                                                                   |  String  |    No     |
| customer_purchase_id  | Order number of the customer                                                                                                                                                                                                                                                                                                                                                                             |  String  |    No     |
| delivery_note_id      | Identification number of the delivery note                                                                                                                                                                                                                                                                                                                                                               |  String  |    Yes    |
| load_order_id         | Identification number of the load order                                                                                                                                                                                                                                                                                                                                                                  |  String  |    Yes    |
| sales_order_id        | Identification number of the sales order                                                                                                                                                                                                                                                                                                                                                                 |  String  |    Yes    |
| cost_center_id        | Cost center or project id of the customer                                                                                                                                                                                                                                                                                                                                                                |  String  |    No     |
| license_plate_truck   | License plate number of the truck                                                                                                                                                                                                                                                                                                                                                                        |  String  |    No     |
| license_plate_trailer | License plate number of the trailer                                                                                                                                                                                                                                                                                                                                                                      |  String  |    No     |
| driver_name           | Driver name                                                                                                                                                                                                                                                                                                                                                                                              |  String  |    No     |
| creation_date         | Naive datetime of delivery note creation <br>*Data format according to ISO-8601/RFC-3339 without time zone: "%Y-%m-%d %H:%M:%S" (e.g. 2020-08-01 01:30:20) or "%Y-%m-%dT%H:%M:%S" (z.B. 2020-08-01T01:30:20). If a timezone is given (e.g. +02:00) an error will be thrown in order to guarantee a correct display.*                                                                                     | Datetime |    Yes    |
| cargo_item_amount     | Amount of items (colli) in the load <br>*Must be a positive number.*                                                                                                                                                                                                                                                                                                                                     | Integer  |    No     |
| text_prefix           | Free text entry between address line and product list                                                                                                                                                                                                                                                                                                                                                    |  String  |    No     |
| text_suffix           | Free text entry between Product list and footer                                                                                                                                                                                                                                                                                                                                                          |  String  |    No     |
| weight_total          | Total weight of the products <br>*Must be a positive number.*                                                                                                                                                                                                                                                                                                                                            |  Float   |    Yes    |
| weight_unit           | Weight unit of the total weight                                                                                                                                                                                                                                                                                                                                                                          |  String  |    Yes    |
| customer              | Data on the customer <br>*For further information, see the **Customer** table below.*                                                                                                                                                                                                                                                                                                                    |  Object  |    Yes    |
| invoice_address       | Data on the invoice address <br>*For further information, see the **Address** table below.*                                                                                                                                                                                                                                                                                                              |  Object  |    Yes    |
| delivery_address      | Data on the delivery address<br>*For further information, see the **Address** table below.*                                                                                                                                                                                                                                                                                                              |  Object  |    Yes    |
| sender_address        | Data on the sender address<br>*For further information, see the **Address** table below.*                                                                                                                                                                                                                                                                                                                |  Object  |    Yes    |
| purchaser             | Data on the purchasing person <br>*For further information, see the **Person** table below.*                                                                                                                                                                                                                                                                                                             |  Object  |    No     |
| receiver              | Data on the contact person, who will receive the delivery <br>*After delivery, the delivery bill is automatically sent to this e-mail address.<br> For further information, see **Person** below.*                                                                                                                                                                                                       |  Object  |    Yes    | 
| products              | List of all products on the delivery note <br>*- The order of the products is maintained. <br>- It is possible to use a product with the same item number more than once. <br>- There will be a validation error if products with the same item number have different units. <br>- There will be a validation error if the amount is <= 0.<br> For further information see the **Product** table below.* |  Object  |    Yes    |

### Customer

| Property    | Description                              | Datatype | Mandatory |
|:------------|:-----------------------------------------|:--------:|:---------:|
| customer_id | Your internal customer identifier        |  String  |    Yes    |
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

### Product

| Property       | Description                                            | Datatype | Mandatory |
|:---------------|:-------------------------------------------------------|:--------:|:---------:|
| amount         | Amount of the product<br/>*Must be a positive number.* |  Float   |    Yes    |
| unit           | Unit of the product                                    |  String  |    Yes    |
| article_id | Article number of the product                          |  String  |    Yes    |
| article_name   | Name of the product                                    |  String  |    Yes    |

### Request payload example

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
  "text_prefix": "Material according to offer Nr. 1238921",
  "text_suffix": "Thank you for your purchase!",
  "weight_total": "1.5",
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
    "address_prefix": "Coffee at the corner",
    "street": "Delivery address",
    "house_nr": "66",
    "zip": "1100",
    "city": "Vienna",
    "country": "Austria",
    "additional_info": "Please come to the back entrance"
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
      "amount": "2",
      "unit": "STK",
      "article_id": "6987324",
      "article_name": "Product XY size 3"
    },
    {
      "amount": "1",
      "unit": "STK",
      "article_id": "6987323",
      "article_name": "Product XY size 2"
    },
    {
      "amount": "500.5",
      "unit": "KG",
      "article_id": "6946722",
      "article_name": "Product YX"
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

If sent data is incomplete or faulty, there will be a 422 response like the following.
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

There was an unexpected error. Please contact support@reebuild.com with the payload, so we can fix this as soon as
possible. 
