---
layout: index
title:  "Sales Receipt Endpoints"
date:   2017-01-26
categories: api-endpoints
---

<header>
<h1>Sales Receipt Endpoints</h1>
</header>

You can manage sales receipts with "salesreceipts" API endpoints, collect revenue from customers.

A sales receipt must have an unique receipt number "receipt_no" 
and some items to sell, where all required fields are listed in **Attributes** below. 

When a sales receipt is created, it will be "PAID". Please sign in Pymlo web system to send it to your customers.

## Overview
| Endpoint                                                        |  Description  |
| -------------                                                   | ----- |
| [GET /businesses/{business_id}/salesreceipts/](#get-businessesbusiness_idsalesreceipts) | Get a list of sales receipts from given business |
| [GET /businesses/{business_id}/partners/{partner_id}/salesreceipts/](#get-businessesbusiness_idpartnerspartner_idsalesreceipts) | Get a list of sales receipts from given partner |
| [GET /businesses/{business_id}/salesreceipts/{salesreceipt_id}/](#get-businessesbusiness_idsalesreceiptssalesreceipt_id) |  Get a specific sales receipt |
| [POST /businesses/{business_id}/partners/{partner_id}/salesreceipts/](#post-businessesbusiness_idpartnerspartner_idsalesreceipts) |  Create a new sales receipt for given partner and business |
| [PUT /businesses/{business_id}/salesreceipts/](#put-businessesbusiness_idsalesreceipts) |  Update an existing sales receipt |
| [DELETE /businesses/{business_id}/salesreceipts/{salesreceipt_id}/](#delete-businessesbusiness_idsalesreceiptssalesreceipt_id) |  Delete a sales receipt |  

## Attributes
| Name                          |  Editable     | Type          | Description                                   |
| -------------                 | -----         | -----         | -----                                         |
| id                            | false         | string        | Unique identifier of a sales receipt. You can use id to interact with specific sales receipt. |
| receipt_no                    | true, required| string        | Unique number of a sales receipt.             |
| date                          | true, required| string        | Date of a sales receipt.                      |
| currency                      | true, required| object        | Curreny used in a sales receipt. Use ISO currency code. You can look up with [Country](https://github.com/pymloaccounting/pymloaccounting.github.io/blob/api-spec/_posts/2017-01-26-Country-Endpoints.md) and [Currency](https://github.com/pymloaccounting/pymloaccounting.github.io/blob/api-spec/_posts/2017-01-26-Currency-Endpoints.md) endpoints or [ISO](https://www.currency-iso.org/en/home/tables/table-a1.html). |
| currency_rate                 | true, required| BigDecimal    | Curreny rate of sales receipt currency vs book keeping currency. |
| ref_no                        | true          | string        | Other related documents like orders, invoices, delivery notes. |
| memo                          | true          | string        | Memo of a sales receipt.                      |
| customer                      | true, required| object        | Businesss partner that this sales receipt is sent to. |
| address_line_1                | false         | string        | First line of customer address.               |
| address_line_2                | false         | string        | Second line of customer address.              |
| payment_account               | true, required| object        | Account of received payment. Use Account endpoints to get your payment account list. |
| payment_method                | true          | string        | How you received the payment. Valid values are as follows: <br /> cash, cheque, credit_card, transfer, Paypal, Omise. |
| status                        | false         | string        | Current sales receipt status.                 |
| discount                      | true          | BigDecimal    | Discount rate(%).                             |
| sub_total                     | false         | BigDecimal    | Sales receipt subtotal amount. Sum of all discounted receipt detail line amounts. |
| tax_total                     | false         | BigDecimal    | Sales receipt total tax amount. Sum of all discounted receipt detail tax amounts. |
| total                         | false         | BigDecimal    | Sales receipt total amount. Sum of sub_total and tax_total. |

Moreover, at least one receipt detail is required to show selling items.

| Name                          |  Editable     | Type          | Description                                   |
| -------------                 | -----         | -----         | -----                                         |
| product                       | true, required| object        | Product to sell in a receipt detail.            |
| description                   | true          | string        | Description of a receipt detail.                |
| quantity                      | true, required| BigDecimal    | Number of products to sell.                   | 
| unit_price                    | true, required| BigDecimal    | Unit price of a product to sell.              |
| line_amount                   | false         | BigDecimal    | quantity multiplies unit_price is line_amount.    |
| tax                           | true          | object        | Tax required when selling a product.          |
| tax_amount                    | false         | BigDecimal    | line_amount multiplies latest tax rate is tax_amount. |
| total_amount                  | false         | BigDecimal    | line_amount adds tax_amount is total_amount.   |


## Details
### GET /businesses/{business_id}/salesreceipts/
List all sales receipts of given business sorted by date. 
### GET /businesses/{business_id}/partners/{partner_id}/salesreceipts/
List all sales receipts of given partner sorted by date. 

You can use "from_date", "to_date", and "receipt_no" as filters.

Default page length is 100. If per_page = 50 and page = 2, the response message will show 101st - 150th sales receipts. 

##### URL parameters
| Name                              | Type          | Description                                   |
| -------------                     | -----         | -----                                         |
| from_date                         | string        | Find only sales receipts created after specific date.<br /> Please use yyyy-MM-dd format, ex. 2015-12-25 |
| to_date                           | string        | Find only sales receipts created before specific date.<br /> Please use yyyy-MM-dd format, ex. 2015-12-25 |
| receipt_no                        | string        | Find sales receipt with matched receipt number.       |
| per_page                          | integer       | Number of sales receipts listed in one response message. Upper limit is 100. |
| page                              | integer       | Page number listed in response message. Start from 0. |

##### Example Request
```JavaScript
curl https://myaccounting.pymlo.com/businesses/dd921fea/salesreceipts?per_page=50&page=2 \

-H "Authorization: Bearer ACCESS_TOKEN"
```

##### Example Response


##### Example Request
```JavaScript
curl https://myaccounting.pymlo.com/businesses/dd921fea/partners/bef8/salesreceipts?from_date=2017-01-01 \

-H "Authorization: Bearer ACCESS_TOKEN"
```

##### Example Response


### GET /businesses/{business_id}/salesreceipts/{salesreceipts_id}/
Get a specific sales receipt.

##### Example Request
```JavaScript
curl https://myaccounting.pymlo.com/businesses/dd921fea/salesreceipts/rc11/ \ 

-H "Authorization: Bearer ACCESS_TOKEN"
```

##### Example Response


### POST /businesses/{business_id}/partners/{partner_id}/salesreceipts/ 
Create a new sales receipt for given partner and business.


##### Example Request
```JavaScript
curl https://myaccounting.pymlo.com/businesses/dd921fea/partners/bef8/salesreceipts/ \
  -H "Authorization: Bearer ACCESS_TOKEN" \
  -H "Content-Type: application/json" \
  -X POST \
  -d {
    "receipt_no": "RCT00000001",
    "date": "2017-01-26",
    "currency": {
        "code": "THB"
    },
    "currenct_rate": 1,
    "payment_account": {
        "id": "o89j"
    },
    "details": [
      {
        "product": {
          "id": "p1m3"
        },
        "quantity": 20,
        "unit_price": 100
      }
    ]
  }
```
##### Example Response


### PUT /businesses/{business_id}/salesreceipts/
Update an existing sales receipt. Please upload **whole receipt data** including unmodified fields. 

##### Example Request
```JavaScript
curl https://myaccounting.pymlo.com/businesses/dd921fea/salesreceipts/ \
  -H "Authorization: Bearer ACCESS_TOKEN" \
  -H "Content-Type: application/json" \
  -X POST \
  -d {
    "id": "rc11",
    "receipt_no": "RCT00000001",
    "date": "2017-01-26",
    "currency": {
        "code": "THB"
    },
    "currenct_rate": 1,
    "payment_account": {
        "id": "o89j"
    },
    "customer": {
        "id": "bef8"
    },
    "details": [
      {
        "product": {
          "id": "p1m3"
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


### DELETE /businesses/{business_id}/salesreceipts/{receipt_id}/
Delete a sales receipt.

##### Example Request
```JavaScript
curl https://myaccounting.pymlo.com/businesses/dd921fea/salesreceipts/ql44/ \
  -H "Authorization: Bearer ACCESS_TOKEN"
  -X DELETE
```

##### Example Response

