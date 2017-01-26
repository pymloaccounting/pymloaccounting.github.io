---
layout: index
title:  "Product Endpoints"
date:   2017-01-25
categories: api-endpoints
---

<header>
<h1>Product Endpoints</h1>
</header>

The management of products to buy/sell is included in "products" API endpoint. A prodcut must have a "name".

For a selling product, "is_selling" is true. "default_revenue_account" and "default_selling_price" are required. 

For a buying product, "is_buying" is true. "default_expense_account" and "default_buying_price" are required. 

Other fields are optional. If you use "code" for managing products, it should be unique.

## Overview
| Endpoint                                                        |  Description  |
| -------------                                                   | ----- |
| [GET /businesses/{business_id}/products/](#get-businessesbusiness_idproducts) | Get a list of products from given business |
| [GET /businesses/{business_id}/products/{product_id}/](#get-businessesbusiness_idproductsproduct_id) |  Get a specific product |
| [POST /businesses/{business_id}/products/](#post-businessesbusiness_idproducts) |  Create a new product for given business |
| [PUT /businesses/{business_id}/products/](#put-businessesbusiness_idproducts) |  Update an existing product |
| [DELETE /businesses/{business_id}/products/{product_id}/](#delete-businessesbusiness_idproductsproduct_id) |  Delete a product |  

## Attributes
| Endpoint                          | Type          | Description                                   |
| -------------                     | -----         | -----                                         |
| id                                | string        | Unique identifier of a product. Read only. You can use id to interact with specific product. |
| name                              | string        | Name of a product.                            |
| code                              | string        | Code in your business to represent a product. |
| description                       | string        | Description of a product.                     |
| is_selling                        | boolean       | True if you are selling this product.         |
| is_buying                         | boolean       | True if you are buying this product.          |
| default_revenue_account           | object        | Default account when selling a product. Please refer to Account Endpoints to get account id. |
| default_selling_price             | BigDecimal    | Default price when selling a product. |
| default_selling_tax               | object        | Default tax when selling a product. Please refer to Tax Endpoints to get tax id. |
| default_expense_account           | object        | Default account when buying a product. Please refer to Account Endpoints to get account id. |
| default_buying_price              | BigDecimal    | Default price when buying a product. |
| default_buying_tax                | object        | Default tax when buying a product. Please refer to Tax Endpoints to get tax id. |

## Details
### GET /businesses/{business_id}/products/
List all products of given business sorted by product name. You can use "is_buy", "is_sell", and "code" as filters.

Default page length is 100. If per_page = 50 and page = 2, the response message will show 101st - 150th products. 

##### URL parameters
| Endpoint                          | Type          | Description                                   |
| -------------                     | -----         | -----                                         |
| is_selling                        | boolean       | True if you want to find only selling products. |
| is_buying                         | boolean       | True if you want to find only buying products. |
| code                              | string        | Find product having matched product code.     |
| per_page                          | integer       | Number of products listed in one response message. Upper limit is 100. |
| page                              | integer       | Page number of products listed in response message. Start from 0. |

##### Example Request
```JavaScript
curl https://myaccounting.pymlo.com/businesses/dd921fea/products?is_buying=true&per_page=50&page=2 \

-H "Authorization: Bearer ACCESS_TOKEN"
```

##### Example Response


### GET /businesses/{business_id}/products/{product_id}/
Get a specific product.

##### Example Request
```JavaScript
curl https://myaccounting.pymlo.com/businesses/dd921fea/products/p1m3/ \ 

-H "Authorization: Bearer ACCESS_TOKEN"
```

##### Example Response


### POST /businesses/{business_id}/products/ 
Create a new product for given business.


##### Example Request
```JavaScript
curl https://myaccounting.pymlo.com/businesses/dd921fea/products/ \
  -H "Authorization: Bearer ACCESS_TOKEN" \
  -H "Content-Type: application/json" \
  -X POST \
  -d {
    "name": "Pancake",
    "is_sell": true,
    "default_revenue_account": {
        "id": o89j
    },
    "default_selling_price": 30
  }
```
##### Example Response


### PUT /businesses/{business_id}/products/
Update an existing product. Please upload **whole product data** including unmodified fields.


##### Example Request
```JavaScript
curl https://myaccounting.pymlo.com/businesses/dd921fea/products/ \
  -H "Authorization: Bearer ACCESS_TOKEN" \
  -H "Content-Type: application/json" \
  -X POST \
  -d {
    "id": p1m3,
    "name": "Pancake",
    "is_sell": true,
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


### DELETE /businesses/{business_id}/products/{product_id}/
Delete a product.


##### Example Request
```JavaScript
curl https://myaccounting.pymlo.com/businesses/dd921fea/products/p1m3/ \
  -H "Authorization: Bearer ACCESS_TOKEN"
  -X DELETE
```

##### Example Response

