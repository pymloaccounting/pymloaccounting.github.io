---
layout: index
title:  "Country Endpoints"
date:   2017-01-26
categories: api-endpoints
---

<header>
<h1>Country Endpoints</h1>
</header>

You can check ISO country codes, country names, and their currencies by "countries" API endpoint. 

## Overview
| Endpoint                                                                          |  Description  |
| -------------                                                                     | -----         |
| [GET /countries/](#get-countries)                                                 | List all country codes and their names  |
| [GET /countries/{country_code}/currencies/](https://github.com/pymloaccounting/pymloaccounting.github.io/blob/api-spec/_posts/2017-01-26-Currency-Endpoints.md#get-countriescountry_codecurrencies) | Get currency of specific country        |

## Attributes
| Name                          | Type          | Description                                   |
| -------------                     | -----         | -----                                         |
| code                              | string        | ISO country code of a country.                |
| name                              | string        | Name of a country. Default is English.        |

## Details
### GET /countries/
List all country codes and their names. You can use "locale" to choose output language, and "name" as filter to find certain country.

##### URL parameters
| Name                              | Type          | Description                                     |
| -------------                     | -----         | -----                                           |
| locale                            | string        | Get country names with specified locale: <br /> en: English<br /> th: Thai<br /> zh: Traditional Chinese<br /> zh_CN: Simplified Chinese             |
| name                              | string        | Find certain country with matched country name. |

##### Example Request
```JavaScript
curl https://myaccounting.pymlo.com/countries?locale=en&name=Thailand \

-H "Authorization: Bearer ACCESS_TOKEN"
```

##### Example Response

