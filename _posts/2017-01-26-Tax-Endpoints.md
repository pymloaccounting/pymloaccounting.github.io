---
layout: index
title:  "Tax Endpoints"
date:   2017-01-26
categories: api-endpoints
---

<header>
<h1>Tax Endpoints</h1>
</header>

You can retrieve existing taxes of your business in "taxes" API endpoint. A tax must have an unique tax code.

## Overview
| Endpoint                                                        |  Description  |
| -------------                                                   | ----- |
| [GET /businesses/{business_id}/taxes/](#get-businessesbusiness_idtaxes) | Get a list of taxes from given business |
| [GET /businesses/{business_id}/taxes/{tax_id}/](#get-businessesbusiness_idtaxestax_id) |  Get a specific tax      |

## Attributes
| Endpoint                          | Type          | Description                                   |
| -------------                     | -----         | -----                                         |
| id                                | string        | Unique identifier of a tax. Read only. You can use id to interact with specific tax. |
| code                              | string        | Code in your business to represent a tax.     |
| name                              | string        | Name of a tax.                                |
| tax_id                            | string        | Tax payer ID.                                 |
| recoverable                       | boolean       | True if it is a recoverable tax.              |
| compound                          | boolean       | True if it is a compound tax.                 |
| withholding                       | boolean       | True if it is a withholding tax.               |

## Details
### GET /businesses/{business_id}/taxes/
List all taxes of given business sorted by tax code. You can use "code" as filter.

##### URL parameters
| Endpoint                          | Type          | Description                                   |
| -------------                     | -----         | -----                                         |
| code                              | string        | Find tax with matched tax code.             |

##### Example Request
```JavaScript
curl https://myaccounting.pymlo.com/businesses/dd921fea/taxes?code=VAT-7 \

-H "Authorization: Bearer ACCESS_TOKEN"
```

##### Example Response


### GET /businesses/{business_id}/taxes/{tax_id}/
Get a specific tax.

##### Example Request
```JavaScript
curl https://myaccounting.pymlo.com/businesses/dd921fea/taxes/ty1n/ \ 

-H "Authorization: Bearer ACCESS_TOKEN"
```

##### Example Response


