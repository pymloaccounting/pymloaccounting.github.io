---
layout: index
title:  "Bill Payment Endpoints"
date:   2017-01-30
categories: api-endpoints
---

<header>
<h1>Bill Payment Endpoints</h1>
</header>

You can manage vendor bill payments with "billpayments" API endpoints, record payments after you paid bills to vendors.

A bill payment must contain amount, date, currency rate, and payment account. If you leave "description" empty, Pymlo will generate one for you as "Payment for vendor bill#" + parent bill number. 

## Overview
| Endpoint                                                        |  Description  |
| -------------                                                   | ----- |
| [GET /businesses/{business_id}/billpayments/](#get-businessesbusiness_idbillpayments) | Get a list of bill payments from given business |
| [GET /businesses/{business_id}/bills/{bill_id}/billpayments/](#get-businessesbusiness_idbillsbill_idbillpayments) | Get a list of bill payments from given vendor bill|
| [GET /businesses/{business_id}/billpayments/{billpayment_id}/](#get-businessesbusiness_idbillpaymentsbillpayment_id) |  Get a specific bill payment |
| [POST /businesses/{business_id}/bills/{bill_id}/billpayments/](#post-businessesbusiness_idbillsbill_idbillpayments) |  Create a new bill payment for given vendor bill |
| [PUT /businesses/{business_id}/billpayments/](#put-businessesbusiness_idbillpayments) |  Update an existing bill payment |
| [DELETE /businesses/{business_id}/billpayments/{billpayment_id}/](#delete-businessesbusiness_idbillpaymentsbillpayment_id) |  Delete an bill payment |  

## Attributes
| Name                          |  Editable     | Type          | Description                                   |
| -------------                 | -----         | -----         | -----                                         |
| id                            | false         | string        | Unique identifier of an bill payment. You can use id to interact with specific payment. |
| date                          | true, required| string        | Date of an bill payment.                    |
| currency_rate                 | true, required| BigDecimal    | Curreny rate of vendor bill currency vs book keeping currency. |
| payment_account               | true, required| object        | The account used to record this payment.      |
| amount                        | true, required| BigDecimal    | Total payment amount.                         |
| description                   | true          | string        | Payment description.                          |

## Details
### GET /businesses/{business_id}/billpayments/
List all bill payments of given business sorted by date. 
### GET /businesses/{business_id}/bills/{bill_id}/billpayments/
List all bill payments of given vendor bill and business sorted by date. 

You can use "from_date" and "to_date" as filters.

Default page length is 100. If per_page = 50 and page = 2, the response message will show 101st - 150th bill payments. 

##### URL parameters
| Name                              | Type          | Description                                   |
| -------------                     | -----         | -----                                         |
| from_date                         | string        | Find only bill payments created after specific date.<br /> Please use yyyy-MM-dd format, ex. 2015-12-25 |
| to_date                           | string        | Find only bill payments created before specific date.<br /> Please use yyyy-MM-dd format, ex. 2015-12-25 |
| per_page                          | integer       | Number of bill payments listed in one response message. Upper limit is 100. |
| page                              | integer       | Page number listed in response message. Start from 0. |

##### Example Request
```JavaScript
curl https://myaccounting.pymlo.com/businesses/dd921fea/billpayments?per_page=50&page=2 \

-H "Authorization: Bearer ACCESS_TOKEN"
```

##### Example Response


##### Example Request
```JavaScript
curl https://myaccounting.pymlo.com/businesses/dd921fea/bills/b731/billpayments?from_date=2017-01-01 \

-H "Authorization: Bearer ACCESS_TOKEN"
```

##### Example Response


### GET /businesses/{business_id}/billpayments/{billpayment_id}/
Get a specific bill payment.

##### Example Request
```JavaScript
curl https://myaccounting.pymlo.com/businesses/dd921fea/billpayments/ep1k/ \ 

-H "Authorization: Bearer ACCESS_TOKEN"
```

##### Example Response


### POST /businesses/{business_id}/bills/{bill_id}/billpayments/
Create a new bill payment for given vendor bill.


##### Example Request
```JavaScript
curl https://myaccounting.pymlo.com/businesses/dd921fea/bills/b731/billpayments/ \
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
    "desription": "Payment for venor bill#B00000001"
  }
```
##### Example Response


### PUT /businesses/{business_id}/billpayments/
Update an existing bill payment. Please upload **whole bill payment data** including unmodified fields. 

##### Example Request
```JavaScript
curl https://myaccounting.pymlo.com/businesses/dd921fea/billpayments/ \
  -H "Authorization: Bearer ACCESS_TOKEN" \
  -H "Content-Type: application/json" \
  -X POST \
  -d {
    "id": "ep1k",
    "date": "2017-01-26",
    "currency_rate": 1,
    "amount": 2000,
    "payment_account": {
        "id": "o89j"
    },
    "desription": "Payment for venor bill#INV00000001"
  }
```

##### Example Response


### DELETE /businesses/{business_id}/billpayments/{billpayment_id}/
Delete an income payment.

##### Example Request
```JavaScript
curl https://myaccounting.pymlo.com/businesses/dd921fea/billpayments/ep1k/ \
  -H "Authorization: Bearer ACCESS_TOKEN"
  -X DELETE
```

##### Example Response
