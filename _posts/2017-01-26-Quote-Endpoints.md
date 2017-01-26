---
layout: index
title:  "Quote Endpoints"
date:   2017-01-26
categories: api-endpoints
---

<header>
<h1>Quote Endpoints</h1>
</header>

You can manage quotations with "quotes" API endpoint, send quotes to negotiate selling price with customers.

A quote must have an unique quote number "quote_no" 
and some items to sell, where all mandatory fields will be listed in **Attributes** below. 

When a quote is created, it will be "Draft". Please sign in Pymlo web system to send it to your customers.

## Overview
| Endpoint                                                        |  Description  |
| -------------                                                   | ----- |
| [GET /businesses/{business_id}/quotes/](#get-businessesbusiness_idquotes) | Get a list of quotes from given business |
| [GET /businesses/{business_id}/partners/{partner_id}/quotes/](#get-businessesbusiness_idpartnerspartner_idquotes) | Get a list of quotes from given partner and business |
| [GET /businesses/{business_id}/quotes/{quote_id}/](#get-businessesbusiness_idquotesquote_id) |  Get a specific quote |
| [POST /businesses/{business_id}/partners/{partner_id}/quotes/](#post-businessesbusiness_idpartnerspartner_idquotes) |  Create a new quote for given partner and business |
| [PUT /businesses/{business_id}/quotes/](#put-businessesbusiness_idquotes) |  Update an existing quote |
| [DELETE /businesses/{business_id}/quotes/{quote_id}/](#delete-businessesbusiness_idquotesquote_id) |  Delete a quote |  

## Attributes
| Name                          |  Editable     | Type          | Description                                   |
| -------------                 | -----         | -----         | -----                                         |
| id                            | false         | string        | Unique identifier of a quote. You can use id to interact with specific quote. |
| quote_no                      | true, required| string        | Unique number of a quote.                     |
| date                          | true, required| string        | Date of a quote.                              |
| due_date                      | true, required| string        | Due date of a quote.                          |
| currency                      | true, required| object        | Curreny used in a quote. Use ISO currency code. You can use Country and Currency endpoints or [ISO](https://www.currency-iso.org/en/home/tables/table-a1.html) to look up currency code. |
| memo                          | true          | string        | Memo of a quote.                              |
| customer                      | true, required| object        | Businesss partner that this quote is sent to. |
| address_line_1                | false         | string        | First line of customer address.               |
| address_line_2                | false         | string        | Second line of customer address.              |
| status                        | false         | string        | Current quote status.                         |
| sub_total                     | false         | BigDecimal    | Quote subtotal amount. Sum of all discounted quote detail line amounts. |
| tax_total                     | false         | BigDecimal    | Quote total tax amount. Sum of all discounted quote detail tax amounts. |
| total                         | false         | BigDecimal    | Quote total amount. Sum of sub_total adds tax_total. |

Moreover, at least one quote detail is required to show selling items.

| Name                          |  Editable     | Type          | Description                                   |
| -------------                 | -----         | -----         | -----                                         |
| product                       | true, required| object        | Product to sell in a quote detail.            |
| description                   | true          | string        | Description of a quote detail.                |
| quantity                      | true, required| BigDecimal    | Number of products to sell.                   | 
| unit_price                    | true, required| BigDecimal    | Unit price of a product to sell.              |
| line_amount                   | false         | BigDecimal    | Product of quantity multiplies unit_price.    |
| tax                           | true          | object        | Tax required when selling a product.          |
| tax_amount                    | false         | BigDecimal    | Product of line_amount multiplies latest tax rate.   |
| total_amount                  | false         | BigDecimal    | Sum of line_amount adds tax_amount.   |


## Details
### GET /businesses/{business_id}/quotes/
List all quotes of given business sorted by date. 
### GET /businesses/{business_id}/partners/{partner_id}/quotes/
List all quotes of given partner and business sorted by date. 

You can use "from_date", "to_date", and "quote_no" as filters.

Default page length is 100. If per_page = 50 and page = 2, the response message will show 101st - 150th quotes. 

##### URL parameters
| Name                              | Type          | Description                                   |
| -------------                     | -----         | -----                                         |
| from_date                         | string        | Find only quotes created after specific date.<br /> Please use yyyy-MM-dd format, ex. 2015-12-25 |
| to_date                           | string        | Find only quotes created before specific date.<br /> Please use yyyy-MM-dd format, ex. 2015-12-25 |
| quote_no                          | string        | Find quote with matched quote number.       |
| per_page                          | integer       | Number of quotes listed in one response message. Upper limit is 100. |
| page                              | integer       | Page number of quotes listed in response message. Start from 0. |

##### Example Request
```JavaScript
curl https://myaccounting.pymlo.com/businesses/dd921fea/quotes?per_page=50&page=2 \

-H "Authorization: Bearer ACCESS_TOKEN"
```

##### Example Response


##### Example Request
```JavaScript
curl https://myaccounting.pymlo.com/businesses/dd921fea/partners/bef8/quotes?from_date=2017-01-01 \

-H "Authorization: Bearer ACCESS_TOKEN"
```

##### Example Response


### GET /businesses/{business_id}/quotes/{quote_id}/
Get a specific quote.

##### Example Request
```JavaScript
curl https://myaccounting.pymlo.com/businesses/dd921fea/quotes/ql44/ \ 

-H "Authorization: Bearer ACCESS_TOKEN"
```

##### Example Response


### POST /businesses/{business_id}/partners/{partner_id}/quotes/ 
Create a new quote for given partner and business.


##### Example Request
```JavaScript
curl https://myaccounting.pymlo.com/businesses/dd921fea/partners/bef8/quotes/ \
  -H "Authorization: Bearer ACCESS_TOKEN" \
  -H "Content-Type: application/json" \
  -X POST \
  -d {
    "quote_no": "QTE00000001",
    "date": "2017-01-26",
    "due_date": "2017-02-26",
    "currency": {
        "code": THB
    },
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


### PUT /businesses/{business_id}/quotes/
Update an existing quote. Please upload **whole quote data** including unmodified fields. 

You can only update quotes with status "Draft" and "Sent".

##### Example Request
```JavaScript
curl https://myaccounting.pymlo.com/businesses/dd921fea/quotes/ \
  -H "Authorization: Bearer ACCESS_TOKEN" \
  -H "Content-Type: application/json" \
  -X POST \
  -d {
    "id": ql44,
    "quote_no": "QTE00000001",
    "date": "2017-01-26",
    "due_date": "2017-02-26",
    "currency": {
        "code": THB
    },
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


### DELETE /businesses/{business_id}/quotes/{quote_id}/
Delete a quote.

You can only delete quotes with status "Draft".

##### Example Request
```JavaScript
curl https://myaccounting.pymlo.com/businesses/dd921fea/quotes/ql44/ \
  -H "Authorization: Bearer ACCESS_TOKEN"
  -X DELETE
```

##### Example Response

