---
layout: index
title:  "Account Endpoints"
date:   2017-01-26
categories: api-endpoints
---

<header>
<h1>Account Endpoints</h1>
</header>

You can take care of chart of accounts of business in "accounts" API endpoint. 

An account must have a "name", a unique "code", and "type".

For detail discussion about accounts in Pymlo, please refer to [Manage Chart of Accounts](https://help.pymlo.com/hc/en-us/articles/225649948-Manage-Chart-of-Accounts)

## Overview
| Endpoint                                                        |  Description  |
| -------------                                                   | ----- |
| [GET /businesses/{business_id}/accounts/](#get-businessesbusiness_idaccounts) | Get a list of accounts from given business |
| [GET /businesses/{business_id}/accounts/{account_id}/](#get-businessesbusiness_idaccountsaccount_id) |  Get a specific account |
| [POST /businesses/{business_id}/accounts/](#post-businessesbusiness_idaccounts) |  Create a new account for given business |
| [PUT /businesses/{business_id}/accounts/](#put-businessesbusiness_idaccounts) |  Update an existing account |
| [DELETE /businesses/{business_id}/accounts/{account_id}/](#delete-businessesbusiness_idaccountsaccount_id) |  Delete an account |  

## Attributes
| Name                              | Type          | Description                                   |
| -------------                     | -----         | -----                                         |
| id                                | string        | Unique identifier of an account. Read only. You can use id to interact with specific account. |
| name                              | string        | Name of an account.                            |
| code                              | string        | Code in your business to represent an account. |
| type                              | string        | Type of an account. Only valid for following: <br /> Assets, Assets -  Current, Assets - Investments, Assets - Fixed Assets, Assets - Other. <br /> Liabilities, Liabilities - Current, Liabilities - Long-term, Liabilities - Other. <br /> Equity. <br /> Revenues, Revenues - Operating, Revenues - Non-Operating. <br /> Expenses, Expenses - Cost of Sales, Expenses - Operating, Expenses - Non-Operating. |
| payment_account                   | boolean       | True if this is a payment account.            |
| contra_account                    | boolean       | True if this is a contra account.             |

## Details
### GET /businesses/{business_id}/accounts/
List all accounts of given business sorted by account code. 

You can use "type", "sub_type", "code", and "payment_account" as filters.

Default page length is 100. If per_page = 50 and page = 2, the response message will show 101st - 150th accounts. 

##### URL parameters
| Name                              | Type          | Description                                   |
| -------------                     | -----         | -----                                         |
| type                              | string        | Find accounts with given major type. Only valid for following: <br /> Assets, Liabilities, Equity, Revenues, Expenses. |
| sub_type                          | string        | Find accounts with given sub type. Each major type has different valid sub types: <br />Assets: Current, Investments, Fixed assets, Other.<br /> Liabilities: Current, Long-term, Other.<br /> Revenues: Operating, Non-Operating.<br /> Expenses: Cost of Sales, Operating, Non-Operating. |
| code                              | string        | Find account having matched account code.     |
| payment_account                   | boolean       | Find accounts which are payment account.     |
| per_page                          | integer       | Number of products listed in one response message. Upper limit is 100. |
| page                              | integer       | Page number of products listed in response message. Start from 0. |

##### Example Request
```JavaScript
curl https://myaccounting.pymlo.com/businesses/dd921fea/accounts?type=assets&sub_type=current \

-H "Authorization: Bearer ACCESS_TOKEN"
```

##### Example Response


### GET /businesses/{business_id}/accounts/{account_id}/
Get a specific account.

##### Example Request
```JavaScript
curl https://myaccounting.pymlo.com/businesses/dd921fea/accounts/a6hj/ \ 

-H "Authorization: Bearer ACCESS_TOKEN"
```

##### Example Response


### POST /businesses/{business_id}/accounts/ 
Create a new account for given business.


##### Example Request
```JavaScript
curl https://myaccounting.pymlo.com/businesses/dd921fea/accounts/ \
  -H "Authorization: Bearer ACCESS_TOKEN" \
  -H "Content-Type: application/json" \
  -X POST \
  -d {
    "name": "Rent revenue",
    "code": "4203",
    "type": "Revenues - Non-operating"
  }
```
##### Example Response


### PUT /businesses/{business_id}/accounts/
Update an existing account. Please upload **whole account data** including unmodified fields.


##### Example Request
```JavaScript
curl https://myaccounting.pymlo.com/businesses/dd921fea/accounts/ \
  -H "Authorization: Bearer ACCESS_TOKEN" \
  -H "Content-Type: application/json" \
  -X POST \
  -d {
    "id": a6hj,
    "name": "Rent revenue",
    "code": "4204",
    "type": "Revenues - Non-Operating"
  }
```

##### Example Response


### DELETE /businesses/{business_id}/accounts/{account_id}/
Delete an account.

##### Example Request
```JavaScript
curl https://myaccounting.pymlo.com/businesses/dd921fea/accounts/a6hj/ \
  -H "Authorization: Bearer ACCESS_TOKEN"
  -X DELETE
```

##### Example Response

