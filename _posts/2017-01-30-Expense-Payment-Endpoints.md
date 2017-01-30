---
layout: index
title:  "Expense Payment Endpoints"
date:   2017-01-30
categories: api-endpoints
---

<header>
<h1>Expense Payment Endpoints</h1>
</header>

You can manage expense payments with "exp_payments" API endpoints, record payments after you paid bills to vendors.

An expense payment must contain amount, date, currency rate, and payment account. If you leave "description" empty, Pymlo will generate one for you as "Payment for vendor bill#" + parent bill number. 

## Overview
| Endpoint                                                        |  Description  |
| -------------                                                   | ----- |
| [GET /businesses/{business_id}/exp_payments/](#get-businessesbusiness_idexp_payments) | Get a list of expense payments from given business |
| [GET /businesses/{business_id}/bills/{bill_id}/exp_payments/](#get-businessesbusiness_idbillsbill_idexp_payments) | Get a list of expense payments from given vendor bill|
| [GET /businesses/{business_id}/exp_payments/{exp_payment_id}/](#get-businessesbusiness_idexp_paymentsexp_payment_id) |  Get a specific expense payment |
| [POST /businesses/{business_id}/bills/{bill_id}/exp_payments/](#post-businessesbusiness_idbillsbill_idexp_payments) |  Create a new expense payment for given vendor bill |
| [PUT /businesses/{business_id}/exp_payments/](#put-businessesbusiness_idexp_payments) |  Update an existing expense payment |
| [DELETE /businesses/{business_id}/exp_payments/{exp_payment_id}/](#delete-businessesbusiness_idexp_paymentsexp_payment_id) |  Delete an expense payment |  

## Attributes
| Name                          |  Editable     | Type          | Description                                   |
| -------------                 | -----         | -----         | -----                                         |
| id                            | false         | string        | Unique identifier of an expense payment. You can use id to interact with specific payment. |
| date                          | true, required| string        | Date of an expense payment.                    |
| currency_rate                 | true, required| BigDecimal    | Curreny rate of vendor bill currency vs book keeping currency. |
| payment_account               | true, required| object        | The account used to record this payment.      |
| amount                        | true, required| BigDecimal    | Total payment amount.                         |
| description                   | true          | string        | Payment description.                          |

## Details
### GET /businesses/{business_id}/exp_payments/
List all expense payments of given business sorted by date. 
### GET /businesses/{business_id}/bills/{bill_id}/exp_payments/
List all expense payments of given vendor bill and business sorted by date. 

You can use "from_date" and "to_date" as filters.

Default page length is 100. If per_page = 50 and page = 2, the response message will show 101st - 150th expense payments. 

##### URL parameters
| Name                              | Type          | Description                                   |
| -------------                     | -----         | -----                                         |
| from_date                         | string        | Find only expense payments created after specific date.<br /> Please use yyyy-MM-dd format, ex. 2015-12-25 |
| to_date                           | string        | Find only expense payments created before specific date.<br /> Please use yyyy-MM-dd format, ex. 2015-12-25 |
| per_page                          | integer       | Number of expense payments listed in one response message. Upper limit is 100. |
| page                              | integer       | Page number listed in response message. Start from 0. |

##### Example Request
```JavaScript
curl https://myaccounting.pymlo.com/businesses/dd921fea/exp_payments?per_page=50&page=2 \

-H "Authorization: Bearer ACCESS_TOKEN"
```

##### Example Response


##### Example Request
```JavaScript
curl https://myaccounting.pymlo.com/businesses/dd921fea/bills/b731/exp_payments?from_date=2017-01-01 \

-H "Authorization: Bearer ACCESS_TOKEN"
```

##### Example Response


### GET /businesses/{business_id}/exp_payments/{exp_payment_id}/
Get a specific expense payment.

##### Example Request
```JavaScript
curl https://myaccounting.pymlo.com/businesses/dd921fea/exp_payments/ep1k/ \ 

-H "Authorization: Bearer ACCESS_TOKEN"
```

##### Example Response


### POST /businesses/{business_id}/bills/{bill_id}/exp_payments/
Create a new expense payment for given vendor bill.


##### Example Request
```JavaScript
curl https://myaccounting.pymlo.com/businesses/dd921fea/bills/b731/exp_payments/ \
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


### PUT /businesses/{business_id}/exp_payments/
Update an existing expense payment. Please upload **whole expense payment data** including unmodified fields. 

##### Example Request
```JavaScript
curl https://myaccounting.pymlo.com/businesses/dd921fea/exp_payments/ \
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


### DELETE /businesses/{business_id}/exp_payments/{exp_payment_id}/
Delete an income payment.

##### Example Request
```JavaScript
curl https://myaccounting.pymlo.com/businesses/dd921fea/exp_payments/ep1k/ \
  -H "Authorization: Bearer ACCESS_TOKEN"
  -X DELETE
```

##### Example Response
