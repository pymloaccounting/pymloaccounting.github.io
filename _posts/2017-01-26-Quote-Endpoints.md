---
layout: index
title:  "Quote Endpoints"
date:   2017-01-26
categories: api-endpoints
---

<header>
<h1>Product Endpoints</h1>
</header>

You can manage quotations with "quotes" API endpoint, send quotes to negotiate selling price with customers.

A quote must have an unique quote number "quote_no" 
and some items to sell, where all mandatory fields will be listed in **Attributes** below. 

When a quote is created, it will be "Draft". Please sign in Pymlo web system to send it to your customers.

## Overview
| Endpoint                                                        |  Description  |
| -------------                                                   | ----- |
| [GET /businesses/{business_id}/quotes/](#get-businessesbusiness_idquotes) | Get a list of quotes from given business |
| [GET /businesses/{business_id}/quotes/{quote_id}/](#get-businessesbusiness_idquotesquotet_id) |  Get a specific quote |
| [POST /businesses/{business_id}/quotes/](#post-businessesbusiness_idquotes) |  Create a new quote for given business |
| [PUT /businesses/{business_id}/quotes/](#put-businessesbusiness_idquotes) |  Update an existing quote |
| [DELETE /businesses/{business_id}/quotes/{quote_id}/](#delete-businessesbusiness_idquotesquote_id) |  Delete a quote |  

## Attributes
| Name                              | Type          | Description                                   |
| -------------                     | -----         | -----                                         |
| id                                | string        | Unique identifier of a product. Read only. You can use id to interact with specific product. |
| name                              | string        | Name of a product.                            |
| code                              | string        | Code in your business to represent a product. |
| description                       | string        | Description of a product.                     |
| sell                              | boolean       | True if you are selling this product.         |
| buy                               | boolean       | True if you are buying this product.          |
| default_revenue_account           | object        | Default account when selling a product. Please refer to Account Endpoints to get account id. |
| default_selling_price             | BigDecimal    | Default price when selling a product. |
| default_selling_tax               | object        | Default tax when selling a product. Please refer to Tax Endpoints to get tax id. |
| default_expense_account           | object        | Default account when buying a product. Please refer to Account Endpoints to get account id. |
| default_buying_price              | BigDecimal    | Default price when buying a product. |
| default_buying_tax                | object        | Default tax when buying a product. Please refer to Tax Endpoints to get tax id. |

## Details
### GET /businesses/{business_id}/quotes/
List all quotes of given business sorted by date created. You can use "from_date", "to_date", and "quote_no" as filters.

Default page length is 100. If per_page = 50 and page = 2, the response message will show 101st - 150th quotes. 

##### URL parameters
| Name                              | Type          | Description                                   |
| -------------                     | -----         | -----                                         |
| from_date                         | string        | Find only quotes created after specific date. |
| to_date                           | string        | Find only quotes created before specific date.|
| quote_no                          | string        | Find quote having matched quote number.       |
| per_page                          | integer       | Number of quotes listed in one response message. Upper limit is 100. |
| page                              | integer       | Page number of quotes listed in response message. Start from 0. |

##### Example Request
```JavaScript
curl https://myaccounting.pymlo.com/businesses/dd921fea/quotes?per_page=50&page=2 \

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


### POST /businesses/{business_id}/quotes/ 
Create a new quote for given business.


##### Example Request
```JavaScript
curl https://myaccounting.pymlo.com/businesses/dd921fea/quotes/ \
  -H "Authorization: Bearer ACCESS_TOKEN" \
  -H "Content-Type: application/json" \
  -X POST \
  -d {
    "quote_no": "QTE00000044",
    
    
    "default_revenue_account": {
        "id": o89j
    },
    "default_selling_price": 30
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
    "name": "Pancake",
    "sell": true,
    "default_revenue_account": {
        "id": o89j
    },
    "default_selling_price": 30,
    "default_selling_tax": {
        "id": ty1n
    }
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

