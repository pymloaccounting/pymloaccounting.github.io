---
layout: index
title:  "Invoice Payment Endpoints"
date:   2017-01-30
categories: api-endpoints
---

<header>
<h1>Invoice Payment Endpoints</h1>
</header>

You can manage invoice payments with "invoicepayments" API endpoints, record payments after customers paid your invoices.

An invoice payment must contain amount, date, currency rate, and payment account. If you leave "description" empty, Pymlo will generate one for you as "Payment for Invoice#" + parent invoice number. 

## Overview
| Endpoint                                                        |  Description  |
| -------------                                                   | ----- |
| [GET /businesses/{business_id}/invoicepayments/](#get-businessesbusiness_idinvoicepayments) | Get a list of invoice payments from given business |
| [GET /businesses/{business_id}/invoices/{invoice_id}/invoicepayments/](#get-businessesbusiness_idinvoicesinvoice_idinvoicepayments) | Get a list of invoice payments from given invoice |
| [GET /businesses/{business_id}/invoicepayments/{invoicepayment_id}/](#get-businessesbusiness_idinvoicepaymentsinvoicepayment_id) |  Get a specific invoice payment |
| [POST /businesses/{business_id}/invoices/{invoice_id}/inc_payments/](#post-businessesbusiness_idinvoicesinvoice_idinvoicepayments) |  Create a new invoice payment for given invoice |
| [PUT /businesses/{business_id}/invoicepayments/](#put-businessesbusiness_idinvoicepayments) |  Update an existing invoice payment |
| [DELETE /businesses/{business_id}/invoicepayments/{invoicepayment_id}/](#delete-businessesbusiness_idinvoicepaymentsinvoicepayment_id) |  Delete an invoice payment |  

## Attributes
| Name                          |  Editable     | Type          | Description                                   |
| -------------                 | -----         | -----         | -----                                         |
| id                            | false         | string        | Unique identifier of an invoice payment. You can use id to interact with specific payment. |
| date                          | true, required| string        | Date of an invoice payment.                    |
| currency_rate                 | true, required| BigDecimal    | Curreny rate of invoice currency vs book keeping currency. |
| payment_account               | true, required| object        | The account used to record this payment.      |
| amount                        | true, required| BigDecimal    | Total payment amount.                         |
| description                   | true          | string        | Payment description.                          |

## Details
### GET /businesses/{business_id}/invoicepayments/
List all invoice payments of given business sorted by date. 
### GET /businesses/{business_id}/invoices/{invoice_id}/invoicepayments/
List all invoice payments of given invoice sorted by date. 

You can use "from_date" and "to_date" as filters.

Default page length is 100. If per_page = 50 and page = 2, the response message will show 101st - 150th invoice payments. 

##### URL parameters
| Name                              | Type          | Description                                   |
| -------------                     | -----         | -----                                         |
| from_date                         | string        | Find only invoice payments created after specific date.<br /> Please use yyyy-MM-dd format, ex. 2015-12-25 |
| to_date                           | string        | Find only invoice payments created before specific date.<br /> Please use yyyy-MM-dd format, ex. 2015-12-25 |
| per_page                          | integer       | Number of invoice payments listed in one response message. Upper limit is 100. |
| page                              | integer       | Page number listed in response message. Start from 0. |

##### Example Request
```JavaScript
curl https://myaccounting.pymlo.com/businesses/dd921fea/invoicepayments?per_page=50&page=2 \

-H "Authorization: Bearer ACCESS_TOKEN"
```

##### Example Response


##### Example Request
```JavaScript
curl https://myaccounting.pymlo.com/businesses/dd921fea/invoices/ib0v/invoicepayments?from_date=2017-01-01 \

-H "Authorization: Bearer ACCESS_TOKEN"
```

##### Example Response


### GET /businesses/{business_id}/invoicepayments/{invoicepayment_id}/
Get a specific invoice payment.

##### Example Request
```JavaScript
curl https://myaccounting.pymlo.com/businesses/dd921fea/invoicepayments/pyu9/ \ 

-H "Authorization: Bearer ACCESS_TOKEN"
```

##### Example Response


### POST /businesses/{business_id}/invoices/{invoice_id}/invoicepayments/
Create a new invoice payment for given invoice.


##### Example Request
```JavaScript
curl https://myaccounting.pymlo.com/businesses/dd921fea/invoices/ib0v/invoicepayments/ \
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


### PUT /businesses/{business_id}/invoicepayments/
Update an existing invoice payment. Please upload **whole invoice payment data** including unmodified fields. 

##### Example Request
```JavaScript
curl https://myaccounting.pymlo.com/businesses/dd921fea/invoicepayments/ \
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


### DELETE /businesses/{business_id}/invoicepayments/{invoicepayment_id}/
Delete an invoice payment.

##### Example Request
```JavaScript
curl https://myaccounting.pymlo.com/businesses/dd921fea/invoicepayments/pyu9/ \
  -H "Authorization: Bearer ACCESS_TOKEN"
  -X DELETE
```

##### Example Response
