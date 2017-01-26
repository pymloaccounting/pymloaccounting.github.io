---
layout: index
title:  "Currency Endpoints"
date:   2017-01-26
categories: api-endpoints
---

<header>
<h1>Currency Endpoints</h1>
</header>

You can check ISO currency codes and corresponding country codes by "currencies" API endpoint. 

## Overview
| Endpoint                                                                          |  Description  |
| -------------                                                                     | -----         |
| [GET /currencies/](#get-currencies)                                               | List all currencies codes and their country codes |
| [GET /countries/{country_code}/currencies/](#get-countriescountry_codecurrencies) | Get currency code of specific country |

## Attributes
| Name                          | Type          | Description                                   |
| -------------                 | -----         | -----                                         |
| code                          | string        | ISO currency code of a currency.              |
| symbol                        | string        | Currency symbol.                              |
| country                       | string        | ISO country code of a currency's country.     |

## Details
### GET /currencies/
List all currencies codes and their country codes.

##### Example Request
```JavaScript
curl https://myaccounting.pymlo.com/currencies/ \

-H "Authorization: Bearer ACCESS_TOKEN"
```

##### Example Response


### GET /countries/{country_code}/currencies/
Find specific currency by country code.

##### Example Request
```JavaScript
curl https://myaccounting.pymlo.com/countries/TH/currencies/ \

-H "Authorization: Bearer ACCESS_TOKEN"
```

##### Example Response



