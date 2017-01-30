---
layout: index
title:  "Purchase Order Endpoints"
date:   2017-01-26
categories: api-endpoints
---

<header>
<h1>Purchase Order Endpoints</h1>
</header>

You can manage purchase orders with "pos" API endpoints, send purchase orders to negotiate buying price with vendors.

A purchase order must have an unique purchase order number "po_no" 
and some items to BUY, where all required fields are listed in **Attributes** below. 

When a purchase order is created, it will be "Draft". Please sign in Pymlo web system to send it to your vendors.

## Overview
| Endpoint                                                        |  Description  |
| -------------                                                   | ----- |
| [GET /businesses/{business_id}/pos/](#get-businessesbusiness_idpos) | Get a list of purchase orders from given business |
| [GET /businesses/{business_id}/partners/{partner_id}/pos/](#get-businessesbusiness_idpartnerspartner_idpos) | Get a list of purchase orders from given partner and business |
| [GET /businesses/{business_id}/pos/{po_id}/](#get-businessesbusiness_idpospo_id) |  Get a specific purchase order |
| [POST /businesses/{business_id}/partners/{partner_id}/pos/](#post-businessesbusiness_idpartnerspartner_idpos) |  Create a new purchase order for given partner and business |
| [PUT /businesses/{business_id}/pos/](#put-businessesbusiness_idpos) |  Update an existing purchase order |
| [DELETE /businesses/{business_id}/pos/{po_id}/](#delete-businessesbusiness_idpospo_id) |  Delete a purchase order |  

## Attributes
| Name                          |  Editable     | Type          | Description                                   |
| -------------                 | -----         | -----         | -----                                         |
| id                            | false         | string        | Unique identifier of a purchase order. You can use id to interact with specific purchase order. |
| po_no                         | true, required| string        | Unique number of a purchase order.                     |
| date                          | true, required| string        | Date of a purchase order.                              |
| currency                      | true, required| object        | Curreny used in a purchase order. Use ISO currency code. You can use Country and Currency endpoints or [ISO](https://www.currency-iso.org/en/home/tables/table-a1.html) to look up currency code. |
| memo                          | true          | string        | Memo of a purchase order.                              |
| vendor                        | true, required| object        | Businesss partner that this purchase order is sent to. |
| address_line_1                | false         | string        | First line of vendor address.                 |
| address_line_2                | false         | string        | Second line of vendor address.                |
| status                        | false         | string        | Current purchase order status.                |
| sub_total                     | false         | BigDecimal    | Purchase order subtotal amount. Sum of all discounted purchase order detail line amounts. |
| tax_total                     | false         | BigDecimal    | Purchase order total tax amount. Sum of all discounted purchase order detail tax amounts. |
| total                         | false         | BigDecimal    | Purchase order total amount. Sum of sub_total and tax_total. |

Moreover, at least one purchase order detail is required to show buying items.

| Name                          |  Editable     | Type          | Description                                   |
| -------------                 | -----         | -----         | -----                                         |
| product                       | true, required| object        | Product to buy in a purchase order detail.    |
| description                   | true          | string        | Description of a purchase order detail.       |
| quantity                      | true, required| BigDecimal    | Number of products to buy.                    | 
| unit_price                    | true, required| BigDecimal    | Unit price of a product to buy.               |
| line_amount                   | false         | BigDecimal    | quantity multiplies unit_price is line_amount.|
| tax                           | true          | object        | Tax required when buying a product.           |
| tax_amount                    | false         | BigDecimal    | line_amount multiplies latest tax rate is tax_amount. |
| total_amount                  | false         | BigDecimal    | Sum of line_amount and tax_amount.            |


## Details
### GET /businesses/{business_id}/pos/
List all purchase orders of given business sorted by date. 
### GET /businesses/{business_id}/partners/{partner_id}/pos/
List all purchase orders of given partner and business sorted by date. 

You can use "from_date", "to_date", and "po_no" as filters.

Default page length is 100. If per_page = 50 and page = 2, the response message will show 101st - 150th purchase orders. 

##### URL parameters
| Name                              | Type          | Description                                   |
| -------------                     | -----         | -----                                         |
| from_date                         | string        | Find only purchase orders created after specific date.<br /> Please use yyyy-MM-dd format, ex. 2015-12-25 |
| to_date                           | string        | Find only purchase orders created before specific date.<br /> Please use yyyy-MM-dd format, ex. 2015-12-25 |
| po_no                             | string        | Find purchase order with matched purchase order number.       |
| per_page                          | integer       | Number of purchase orders listed in one response message. Upper limit is 100. |
| page                              | integer       | Page number of purchase orders listed in response message. Start from 0. |

##### Example Request
```JavaScript
curl https://myaccounting.pymlo.com/businesses/dd921fea/pos?per_page=50&page=2 \

-H "Authorization: Bearer ACCESS_TOKEN"
```

##### Example Response


##### Example Request
```JavaScript
curl https://myaccounting.pymlo.com/businesses/dd921fea/partners/bef8/pos?from_date=2017-01-01 \

-H "Authorization: Bearer ACCESS_TOKEN"
```

##### Example Response


### GET /businesses/{business_id}/pos/{po_id}/
Get a specific purchase order.

##### Example Request
```JavaScript
curl https://myaccounting.pymlo.com/businesses/dd921fea/pos/p0as/ \ 

-H "Authorization: Bearer ACCESS_TOKEN"
```

##### Example Response


### POST /businesses/{business_id}/partners/{partner_id}/pos/ 
Create a new purchase order for given partner and business.


##### Example Request
```JavaScript
curl https://myaccounting.pymlo.com/businesses/dd921fea/partners/bef8/pos/ \
  -H "Authorization: Bearer ACCESS_TOKEN" \
  -H "Content-Type: application/json" \
  -X POST \
  -d {
    "po_no": "PO00000001",
    "date": "2017-01-26",
    "currency": {
        "code": THB
    },
    "details": [
      {
        "product": {
          "id": p1m4
        },
        "quantity": 20,
        "unit_price": 100
      }
    ]
  }
```
##### Example Response


### PUT /businesses/{business_id}/pos/
Update an existing purchase order. Please upload **whole purchase order data** including unmodified fields. 

You can only update purchase orders with status "Draft" and "Sent".

##### Example Request
```JavaScript
curl https://myaccounting.pymlo.com/businesses/dd921fea/pos/ \
  -H "Authorization: Bearer ACCESS_TOKEN" \
  -H "Content-Type: application/json" \
  -X POST \
  -d {
    "id": p0as,
    "po_no": "PO00000001",
    "date": "2017-01-26",
    "currency": {
        "code": THB
    },
    "customer": {
        "id": bef8
    },
    "details": [
      {
        "product": {
          "id": p1m4
        },
        "quantity": 20,
        "unit_price": 100
      },
      {
        "product": {
          "id": p8lk
        },
        "quantity": 5,
        "unit_price": 400
        "tax": {
          "id": ty1n
        },
      }
    ]
  }
```

##### Example Response


### DELETE /businesses/{business_id}/pos/{po_id}/
Delete a purchase order.

You can only delete purchase orders with status "Draft".

##### Example Request
```JavaScript
curl https://myaccounting.pymlo.com/businesses/dd921fea/pos/p0as/ \
  -H "Authorization: Bearer ACCESS_TOKEN"
  -X DELETE
```

##### Example Response

