---
layout: index
title:  "Income Payment Endpoints"
date:   2017-01-30
categories: api-endpoints
---

<header>
<h1>Income Payment Endpoints</h1>
</header>

You can manage income payments with "inc_payments" API endpoints, record payments after customers paid your invoices.

An income payment must contain amount, date, currency rate, and payment account. If you leave "description" empty, Pymlo will generate one for you as "Payment for Invoice#" + parent invoice number. 

## Overview
| Endpoint                                                        |  Description  |
| -------------                                                   | ----- |
| [GET /businesses/{business_id}/inc_payments/](#get-businessesbusiness_idinc_payments) | Get a list of income payments from given business |
| [GET /businesses/{business_id}/invoices/{invoice_id}/inc_payments/](#get-businessesbusiness_idinvoicesinvoice_idinc_payments) | Get a list of income payments from given invoice |
| [GET /businesses/{business_id}/inc_payments/{inc_payment_id}/](#get-businessesbusiness_idinc_paymentsinc_payment_id) |  Get a specific income payment |
| [POST /businesses/{business_id}/invoices/{invoice_id}/inc_payments/](#post-businessesbusiness_idinvoicesinvoice_idinc_payments) |  Create a new income payment for given invoice |
| [PUT /businesses/{business_id}/inc_payments/](#put-businessesbusiness_idinc_payments) |  Update an existing income payment |
| [DELETE /businesses/{business_id}/inc_payments/{inc_payment_id}/](#delete-businessesbusiness_idinc_paymentsinc_payment_id) |  Delete an income payment |  

## Attributes
| Name                          |  Editable     | Type          | Description                                   |
| -------------                 | -----         | -----         | -----                                         |
| id                            | false         | string        | Unique identifier of an income payment. You can use id to interact with specific income payment. |
| date                          | true, required| string        | Date of an income payment.                    |
| currency_rate                 | true, required| BigDecimal    | Curreny rate of invoice currency vs book keeping currency. |
| payment_account               | true, required| object        | The account used to record this payment.      |
| amount                        | true, required| BigDecimal    | Total payment amount.                         |
| description                   | true          | string        | Payment description.                          |

## Details
### GET /businesses/{business_id}/inc_payments/
List all income payments of given business sorted by date. 
### GET /businesses/{business_id}/invoices/{invoice_id}/inc_payments/
List all income payments of given invoice and business sorted by date. 

You can use "from_date" and "to_date" as filters.

Default page length is 100. If per_page = 50 and page = 2, the response message will show 101st - 150th income payments. 

##### URL parameters
| Name                              | Type          | Description                                   |
| -------------                     | -----         | -----                                         |
| from_date                         | string        | Find only income payments created after specific date.<br /> Please use yyyy-MM-dd format, ex. 2015-12-25 |
| to_date                           | string        | Find only income payments created before specific date.<br /> Please use yyyy-MM-dd format, ex. 2015-12-25 |
| per_page                          | integer       | Number of income payments listed in one response message. Upper limit is 100. |
| page                              | integer       | Page number listed in response message. Start from 0. |

##### Example Request
```JavaScript
curl https://myaccounting.pymlo.com/businesses/dd921fea/inc_payments?per_page=50&page=2 \

-H "Authorization: Bearer ACCESS_TOKEN"
```

##### Example Response


##### Example Request
```JavaScript
curl https://myaccounting.pymlo.com/businesses/dd921fea/invoices/ib0v/inc_payments?from_date=2017-01-01 \

-H "Authorization: Bearer ACCESS_TOKEN"
```

##### Example Response


### GET /businesses/{business_id}/inc_payments/{inc_payment_id}/
Get a specific income payment.

##### Example Request
```JavaScript
curl https://myaccounting.pymlo.com/businesses/dd921fea/inc_payments/pyu9/ \ 

-H "Authorization: Bearer ACCESS_TOKEN"
```

##### Example Response


### POST /businesses/{business_id}/invoices/{invoice_id}/inc_payments/
Create a new income payment for given invoice.


##### Example Request
```JavaScript
curl https://myaccounting.pymlo.com/businesses/dd921fea/invoices/ib0v/inc_payments/ \
  -H "Authorization: Bearer ACCESS_TOKEN" \
  -H "Content-Type: application/json" \
  -X POST \
  -d {
    "date": "2017-01-26",
    "currency_rate": 1,
    "amount": 1000,
    "payment_account": {
        "id": "o89j"
    },
    "desription": "Payment for Invoice#INV00000001"
  }
```
##### Example Response


### PUT /businesses/{business_id}/inc_payments/
Update an existing income payment. Please upload **whole income payment data** including unmodified fields. 

##### Example Request
```JavaScript
curl https://myaccounting.pymlo.com/businesses/dd921fea/inc_payments/ \
  -H "Authorization: Bearer ACCESS_TOKEN" \
  -H "Content-Type: application/json" \
  -X POST \
  -d {
    "id": "pyu9",
    "date": "2017-01-26",
    "currency_rate": 1,
    "amount": 2000,
    "payment_account": {
        "id": "o89j"
    },
    "desription": "Payment for Invoice#INV00000001"
  }
```

##### Example Response


### DELETE /businesses/{business_id}/inc_payments/{inc_payment_id}/
Delete an income payment.

##### Example Request
```JavaScript
curl https://myaccounting.pymlo.com/businesses/dd921fea/inc_payments/pyu9/ \
  -H "Authorization: Bearer ACCESS_TOKEN"
  -X DELETE
```

##### Example Response
