---
layout: index
title:  "Vendor Bill Endpoints"
date:   2017-01-30
categories: api-endpoints
---

<header>
<h1>Vendor Bill Endpoints</h1>
</header>

You can manage vendor bills with "bills" API endpoints, send vendor bills to make purchase from vendors.

A vendor bill must have an unique bill number "bill_no" 
and some items to buy, where all required fields are listed in **Attributes** below. 

When a vendor bill is created, it will be "Outstanding". 

## Overview
| Endpoint                                                        |  Description  |
| -------------                                                   | ----- |
| [GET /businesses/{business_id}/bills/](#get-businessesbusiness_idbills) | Get a list of vendor bills from given business |
| [GET /businesses/{business_id}/partners/{partner_id}/bills/](#get-businessesbusiness_idpartnerspartner_idbills) | Get a list of vendor bills from given partner |
| [GET /businesses/{business_id}/bills/{bill_id}/](#get-businessesbusiness_idbillsbill_id) |  Get a specific vendor bill |
| [POST /businesses/{business_id}/partners/{partner_id}/bills/](#post-businessesbusiness_idpartnerspartner_idbills) |  Create a new vendor bill for given partner and business |
| [PUT /businesses/{business_id}/bills/](#put-businessesbusiness_idbills) |  Update an existing vendor bill |
| [DELETE /businesses/{business_id}/bills/{bill_id}/](#delete-businessesbusiness_idbillsbill_id) |  Delete a vendor bill |  

Moreover, you can go through bills API to access payments belonging to certain vendor bill:

| Endpoint                                                        |  Description  |
| -------------                                                   | ----- |
| [/businesses/{business_id}/bills/{bill_id}/exp_payments/](https://github.com/pymloaccounting/pymloaccounting.github.io/blob/api-spec/_posts/2017-01-30-Expense-Payment-Endpoints.md)   | Deal with payments belonging to specified vendor bill |


## Attributes
| Name                          |  Editable     | Type          | Description                                   |
| -------------                 | -----         | -----         | -----                                         |
| id                            | false         | string        | Unique identifier of a vendor bill. You can use id to interact with specific vendor bill. |
| bill_no                       | true, required| string        | Unique number of a vendor bill.                  |
| date                          | true, required| string        | Date of a vendor bill.                           |
| due_date                      | true, required| string        | Due date of a vendor bill.                       |
| currency                      | true, required| object        | Curreny used in a vendor bill. Use ISO currency code. You can look up with [Country](https://github.com/pymloaccounting/pymloaccounting.github.io/blob/api-spec/_posts/2017-01-26-Country-Endpoints.md) and [Currency](https://github.com/pymloaccounting/pymloaccounting.github.io/blob/api-spec/_posts/2017-01-26-Currency-Endpoints.md) endpoints or [ISO](https://www.currency-iso.org/en/home/tables/table-a1.html). |
| currency_rate                 | true, required| BigDecimal    | Curreny rate of vendor bill currency vs book keeping currency. |
| po_so_no                      | true          | string        | Purchase order/shipping order number.         |
| memo                          | true          | string        | Message for vendor.                           |
| vendor                        | true, required| object        | Businesss partner that this vendor bill is sent to. |
| address_line_1                | false         | string        | First line of vendor address.                 |
| address_line_2                | false         | string        | Second line of vendor address.                |
| status                        | false         | string        | Current vendor bill status.                   |
| discount                      | true          | BigDecimal    | Discount rate(%).                             |
| sub_total                     | false         | BigDecimal    | Vendor bill subtotal amount. Sum of all discounted bill detail line amounts. |
| tax_total                     | false         | BigDecimal    | Vendor bill total tax amount. Sum of all discounted bill detail tax amounts. |
| total                         | false         | BigDecimal    | Vendor bill total amount. Sum of sub_total and tax_total. |
| paid_amount                   | false         | BigDecimal    | Total bill payment paid.               |
| due_amount                    | false         | BigDecimal    | total subtract paid_amount is due_amount.     |

Moreover, at least one bill detail is required to show buying items.

| Name                          |  Editable     | Type          | Description                                   |
| -------------                 | -----         | -----         | -----                                         |
| product                       | true, required| object        | Product to sell in a bill detail.             |
| description                   | true          | string        | Description of a bill detail.                 |
| quantity                      | true, required| BigDecimal    | Number of products to buy.                    | 
| unit_price                    | true, required| BigDecimal    | Unit price of a product to buy.               |
| line_amount                   | false         | BigDecimal    | quantity multiplies unit_price is line_amount.|
| tax                           | true          | object        | Tax required when buying a product.           |
| tax_amount                    | false         | BigDecimal    | line_amount multiplies latest tax rate is tax_amount. |
| total_amount                  | false         | BigDecimal    | Sum of line_amount and tax_amount.            |


## Details
### GET /businesses/{business_id}/bills/
List all vendor bills of given business sorted by date. 
### GET /businesses/{business_id}/partners/{partner_id}/bills/
List all vendor bills of given partner sorted by date. 

You can use "from_date", "to_date", and "bill_no" as filters.

Default page length is 100. If per_page = 50 and page = 2, the response message will show 101st - 150th vendor bills. 

##### URL parameters
| Name                              | Type          | Description                                   |
| -------------                     | -----         | -----                                         |
| from_date                         | string        | Find only vendor bills created after specific date.<br /> Please use yyyy-MM-dd format, ex. 2015-12-25 |
| to_date                           | string        | Find only vendor bills created before specific date.<br /> Please use yyyy-MM-dd format, ex. 2015-12-25 |
| bill_no                           | string        | Find vendor bill with matched bill number.     |
| per_page                          | integer       | Number of vendor bills listed in one response message. Upper limit is 100. |
| page                              | integer       | Page number listed in response message. Start from 0. |

##### Example Request
```JavaScript
curl https://myaccounting.pymlo.com/businesses/dd921fea/bills?per_page=50&page=2 \

-H "Authorization: Bearer ACCESS_TOKEN"
```

##### Example Response


##### Example Request
```JavaScript
curl https://myaccounting.pymlo.com/businesses/dd921fea/partners/bef8/bills?from_date=2017-01-01 \

-H "Authorization: Bearer ACCESS_TOKEN"
```

##### Example Response


### GET /businesses/{business_id}/bills/{bill_id}/
Get a specific vendor bill.

##### Example Request
```JavaScript
curl https://myaccounting.pymlo.com/businesses/dd921fea/bills/b731/ \ 

-H "Authorization: Bearer ACCESS_TOKEN"
```

##### Example Response


### POST /businesses/{business_id}/partners/{partner_id}/bills/ 
Create a new vendor bill for given partner and business.


##### Example Request
```JavaScript
curl https://myaccounting.pymlo.com/businesses/dd921fea/partners/bef8/bills/ \
  -H "Authorization: Bearer ACCESS_TOKEN" \
  -H "Content-Type: application/json" \
  -X POST \
  -d {
    "bill_no": "B00000001",
    "date": "2017-01-26",
    "due_date": "2017-02-26",
    "currency": {
        "code": "THB"
    },
    "currency_rate": 1,
    "details": [
      {
        "product": {
          "id": "o89j"
        },
        "quantity": 20,
        "unit_price": 100
      }
    ]
  }
```
##### Example Response


### PUT /businesses/{business_id}/bills/
Update an existing vendor bill. Please upload **whole vendor bill data** including unmodified fields. 

You can only update vendor bills with status "Outstanding".

##### Example Request
```JavaScript
curl https://myaccounting.pymlo.com/businesses/dd921fea/bills/ \
  -H "Authorization: Bearer ACCESS_TOKEN" \
  -H "Content-Type: application/json" \
  -X POST \
  -d {
    "id": "b731",
    "bill_no": "B00000001",
    "date": "2017-01-26",
    "due_date": "2017-02-26",
    "currency": {
        "code": "THB"
    },
    "currency_rate": 1,
    "customer": {
        "id": "bef8"
    },
    "details": [
      {
        "product": {
          "id": "o89j"
        },
        "quantity": 20,
        "unit_price": 100
      },
      {
        "product": {
          "id": "p7lk"
        },
        "quantity": 5,
        "unit_price": 400,
        "tax": {
          "id": "ty1n"
        }
      }
    ]
  }
```

##### Example Response


### DELETE /businesses/{business_id}/bills/{bill_id}/
Delete an vendor bill.

You can only delete vendor bills with status "Outstanding", "Paid Partially", and "Overdue".

##### Example Request
```JavaScript
curl https://myaccounting.pymlo.com/businesses/dd921fea/bills/b731/ \
  -H "Authorization: Bearer ACCESS_TOKEN"
  -X DELETE
```

##### Example Response
