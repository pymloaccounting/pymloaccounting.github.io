---
layout: index
title:  "Invoice Endpoints"
date:   2017-01-26
categories: api-endpoints
---

<header>
<h1>Invoice Endpoints</h1>
</header>

You can manage invoices with "invoices" API endpoints, send invoices to collect revenue from customers.

An invoice must have an unique invoice number "invoice_no" 
and some items to sell, where all required fields are listed in **Attributes** below. 

When an invoice is created, it will be "Draft". Please sign in Pymlo web system to send it to your customers.

## Overview
| Endpoint                                                        |  Description  |
| -------------                                                   | ----- |
| [GET /businesses/{business_id}/invoices/](#get-businessesbusiness_idinvoices) | Get a list of invoices from given business |
| [GET /businesses/{business_id}/partners/{partner_id}/invoices/](#get-businessesbusiness_idpartnerspartner_idinvoices) | Get a list of invoices from given partner and business |
| [GET /businesses/{business_id}/invoices/{invoice_id}/](#get-businessesbusiness_idinvoicesinvoice_id) |  Get a specific invoice |
| [POST /businesses/{business_id}/partners/{partner_id}/invoices/](#post-businessesbusiness_idpartnerspartner_idinvoices) |  Create a new invoice for given partner and business |
| [PUT /businesses/{business_id}/invoices/](#put-businessesbusiness_idinvoices) |  Update an existing invoice |
| [DELETE /businesses/{business_id}/invoices/{invoice_id}/](#delete-businessesbusiness_idinvoicesinvoice_id) |  Delete an invoice |  

Moreover, you can go through invoices API to access payements belonging to certain invoice:

| Endpoint                                                        |  Description  |
| -------------                                                   | ----- |
| /businesses/{business_id}/invoices/{invoice_id}/inc_payments/   | Deal with payments belonging to specified invoice |


## Attributes
| Name                          |  Editable     | Type          | Description                                   |
| -------------                 | -----         | -----         | -----                                         |
| id                            | false         | string        | Unique identifier of an invoice. You can use id to interact with specific invoice. |
| invoice_no                    | true, required| string        | Unique number of an invoice.                  |
| date                          | true, required| string        | Date of an invoice.                           |
| due_date                      | true, required| string        | Due date of an invoice.                       |
| currency                      | true, required| object        | Curreny used in an invoice. Use ISO currency code. You can use Country and Currency endpoints or [ISO](https://www.currency-iso.org/en/home/tables/table-a1.html) to look up currency code. |
| currency_rate                 | true, required| BigDecimal    | Curreny rate of invoice currency vs book keeping currency. |
| po_so_no                      | true          | string        | Purchase order/shipping order number.         |
| memo                          | true          | string        | Memo of a sales receipt.                      |
| customer                      | true, required| object        | Businesss partner that this sales receipt is sent to. |
| address_line_1                | false         | string        | First line of customer address.               |
| address_line_2                | false         | string        | Second line of customer address.              |
| status                        | false         | string        | Current invoice status.                       |
| discount                      | true          | BigDecimal    | Discount rate(%).                             |
| sub_total                     | false         | BigDecimal    | Invoice subtotal amount. Sum of all discounted invoice detail line amounts. |
| tax_total                     | false         | BigDecimal    | Invoice total tax amount. Sum of all discounted invoice detail tax amounts. |
| total                         | false         | BigDecimal    | Invoice total amount. Sum of sub_total and tax_total. |
| paid_amount                   | false         | BigDecimal    | Total invoice payment received.               |
| due_amount                    | false         | BigDecimal    | total subtract paid_amount is due_amount.     |

Moreover, at least one invoice detail is required to show selling items.

| Name                          |  Editable     | Type          | Description                                   |
| -------------                 | -----         | -----         | -----                                         |
| product                       | true, required| object        | Product to sell in a invoice detail.          |
| description                   | true          | string        | Description of a invoice detail.              |
| quantity                      | true, required| BigDecimal    | Number of products to sell.                   | 
| unit_price                    | true, required| BigDecimal    | Unit price of a product to sell.              |
| line_amount                   | false         | BigDecimal    | quantity multiplies unit_price is line_amount.|
| tax                           | true          | object        | Tax required when selling a product.          |
| tax_amount                    | false         | BigDecimal    | line_amount multiplies latest tax rate is tax_amount. |
| total_amount                  | false         | BigDecimal    | Sum of line_amount and tax_amount.            |


## Details
### GET /businesses/{business_id}/invoices/
List all invoices of given business sorted by date. 
### GET /businesses/{business_id}/partners/{partner_id}/invoices/
List all invoices of given partner and business sorted by date. 

You can use "from_date", "to_date", and "invoice_no" as filters.

Default page length is 100. If per_page = 50 and page = 2, the response message will show 101st - 150th invoices. 

##### URL parameters
| Name                              | Type          | Description                                   |
| -------------                     | -----         | -----                                         |
| from_date                         | string        | Find only invoices created after specific date.<br /> Please use yyyy-MM-dd format, ex. 2015-12-25 |
| to_date                           | string        | Find only invoices created before specific date.<br /> Please use yyyy-MM-dd format, ex. 2015-12-25 |
| invoice_no                        | string        | Find invoice with matched invoice number.     |
| per_page                          | integer       | Number of invoices listed in one response message. Upper limit is 100. |
| page                              | integer       | Page number of invoices listed in response message. Start from 0. |

##### Example Request
```JavaScript
curl https://myaccounting.pymlo.com/businesses/dd921fea/invoices?per_page=50&page=2 \

-H "Authorization: Bearer ACCESS_TOKEN"
```

##### Example Response


##### Example Request
```JavaScript
curl https://myaccounting.pymlo.com/businesses/dd921fea/partners/bef8/invoices?from_date=2017-01-01 \

-H "Authorization: Bearer ACCESS_TOKEN"
```

##### Example Response


### GET /businesses/{business_id}/invoices/{invoice_id}/
Get a specific invoice.

##### Example Request
```JavaScript
curl https://myaccounting.pymlo.com/businesses/dd921fea/invoices/ib0v/ \ 

-H "Authorization: Bearer ACCESS_TOKEN"
```

##### Example Response


### POST /businesses/{business_id}/partners/{partner_id}/invoices/ 
Create a new invoice for given partner and business.


##### Example Request
```JavaScript
curl https://myaccounting.pymlo.com/businesses/dd921fea/partners/bef8/invoices/ \
  -H "Authorization: Bearer ACCESS_TOKEN" \
  -H "Content-Type: application/json" \
  -X POST \
  -d {
    "invoice_no": "INV00000001",
    "date": "2017-01-26",
    "due_date": "2017-02-26",
    "currency": {
        "code": THB
    },
    "currency_rate": 1,
    "details": [
      {
        "product": {
          "id": o89j
        },
        "quantity": 20,
        "unit_price": 100
      }
    ]
  }
```
##### Example Response


### PUT /businesses/{business_id}/invoices/
Update an existing invoice. Please upload **whole invoice data** including unmodified fields. 

You can only update invoices with status "Draft".

##### Example Request
```JavaScript
curl https://myaccounting.pymlo.com/businesses/dd921fea/invoices/ \
  -H "Authorization: Bearer ACCESS_TOKEN" \
  -H "Content-Type: application/json" \
  -X POST \
  -d {
    "id": ib0v,
    "invoice_no": "INV00000001",
    "date": "2017-01-26",
    "due_date": "2017-02-26",
    "currency": {
        "code": THB
    },
    "currency_rate": 1,
    "customer": {
        "id": bef8
    },
    "details": [
      {
        "product": {
          "id": o89j
        },
        "quantity": 20,
        "unit_price": 100
      },
      {
        "product": {
          "id": p7lk
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


### DELETE /businesses/{business_id}/invoices/{invoice_id}/
Delete an invoice.

You can only delete invoices with status "Draft".

##### Example Request
```JavaScript
curl https://myaccounting.pymlo.com/businesses/dd921fea/invoices/ib0v/ \
  -H "Authorization: Bearer ACCESS_TOKEN"
  -X DELETE
```

##### Example Response
