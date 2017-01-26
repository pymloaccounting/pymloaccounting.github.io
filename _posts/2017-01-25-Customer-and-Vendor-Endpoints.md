---
layout: index
title:  "Customer and Vendor Endpoints"
date:   2017-01-25
categories: api-endpoints
---

<header>
<h1>Customer and Vendor Endpoints</h1>
</header>

The management of customers and vendors is included in business "partners" API endpoint. A partner must have a "name", 
where other fields are optional. If you use "code" for managing partners, it should be unique.

## Overview
| Endpoint                                                        |  Description  |
| -------------                                                   | ----- |
| [GET /businesses/{business_id}/partners/](#get-businessesbusiness_idpartners)  | Get a list of business partners from given business |
| [GET /businesses/{business_id}/partners/{partner_id}/](#get-businessesbusiness_idpartnerspartner_id) |  Get a specific business partner |
| [POST /businesses/{business_id}/partners/](#post-businessesbusiness_idpartners) |  Create a new business partner for given business |
| [PUT /businesses/{business_id}/partners/](#put-businessesbusiness_idpartners) |  Update an existing business partner |
| [DELETE /businesses/{business_id}/partners/{partner_id}/](#delete-businessesbusiness_idpartnerspartner_id) |  Delete a business partner |  

Moreover, you can go through partners API to access related documents: 

| Endpoint                                                        |  Description  |
| -------------                                                   | ----- |
| /businesses/{business_id}/partners/{partner_id}/quotes/         |  Deal with quotes sent to a business partner |
| /businesses/{business_id}/partners/{partner_id}/invoices/       |  Deal with invoices sent to a business partner |
| /businesses/{business_id}/partners/{partner_id}/receipts/       |  Deal with receipts paid by a business partner |
| /businesses/{business_id}/partners/{partner_id}/pos/            |  Deal with purchase orders sent to a business partner |
| /businesses/{business_id}/partners/{partner_id}/bills/          |  Deal with vendor bills paid to a business partner |
| /businesses/{business_id}/partners/{partner_id}/expenses/       |  Deal with expenses paid to a business partner |

## Attributes
| Endpoint                          | Type          | Description                                   |
| -------------                     | -----         | -----                                         |
| id                                | string        | Unique identifier of a partner. Read only. You can use id to interact with specific business partner. |
| name                              | string        | Name of a business partner.                   |
| code                              | string        | Code in your business to represent a partner. |
| customer                          | boolean       | True if you sell product to a partner.        |
| vendor                            | boolean       | True if you buy product from a partner.       |
| default_selling_currency          | string        | Default currency when selling to a partner. Use ISO currency code. |
| default_buying_currency           | string        | Default currency when buying from a partner. Use ISO currency code. |
| contact_name                      | string        | The person you contact with when interacting with a business partner. |
| business_id                       | string        | Business id of a partner.                     |
| phone                             | string        | Phone number of a partner.                    |
| fax                               | string        | Fax number of a partner.                      |
| website                           | string        | Website of a partner.                         |
| email                             | string        | Email of a partner.                           |
| note                              | string        | Any note to describe a partner.               |
| head_quarter                      | boolean       | True if a partner is the head quarter of business.|
| billing_site_number               | string        | If a partner is a branch of larger business, specify branch number. |
| billing_addr_line1                | string        | First line of partner address that you send quotes and invoices to. |
| billing_addr_line2                | string        | Second line of partner address that you send quotes and invoices to. |
| billing_addr_city                 | string        | City of partner address that you send quotes and invoices to. |
| billing_addr_province             | string        | Province of partner address that you send quotes and invoices to. |
| billing_addr_postal_code          | string        | Postal code of partner address that you send quotes and invoices to. |
| billing_addr_country_id           | string        | Country code of partner address that you send quotes and invoices to. Use ISO country code. |
| ship_to_contact_name              | string        | If you need shipping goods to customer, fill the contact person to receive in this field. |
| shipping_addr_line1               | string        | First line of partner address that will receive shipping goods. |
| shipping_addr_line2               | string        | Second line of partner address that will receive shipping goods.|
| shipping_addr_city                | string        | City of partner address that will receive shipping goods. |
| shipping_addr_province            | string        | Province of partner address that will receive shipping goods. |
| shipping_addr_postal_code         | string        | Postal code of partner address that will receive shipping goods. |
| shipping_addr_country_id          | string        | Country code of partner address that will receive shipping goods. Use ISO country code. |
| vendor_addr_line1                 | string        | First line of partner address that you buy products/services from. |
| vendor_addr_line2                 | string        | Second line of partner address that you buy products/services from. |
| vendor_addr_city                  | string        | City of partner address that you buy products/services from. |
| vendor_addr_province              | string        | Province of partner address that you buy products/services from. |
| vendor_addr_postal_code           | string        | Postal code of partner address that you buy products/services from. |
| vendor_addr_country_id            | string        | Country code of partner address that you buy products/services from. Use ISO country code. |


## Details
### GET /businesses/{business_id}/partners/
List all business partners of given business sorted by partner name. Default page length is 100. If per_page = 50 and page = 2, the response message will show 101st - 150th partners. 
##### URL parameters
| Endpoint                          | Type          | Description                                   |
| -------------                     | -----         | -----                                         |
| per_page                          | integer       | Number of partners listed in one response message. Upper limit is 100. |
| page                              | integer       | Page number of partners listed in response message. Start from 0. |

##### Example Request
```JavaScript
curl https://myaccounting.pymlo.com/businesses/dd921fea/partners?per_page=50&page=2 \

-H "Authorization: Bearer ACCESS_TOKEN"
```

##### Example Response


### GET /businesses/{business_id}/partners/{partner_id}/
Get a specific business partner.

##### Example Request
```JavaScript
curl https://myaccounting.pymlo.com/businesses/dd921fea/partners/bef8/ \ 

-H "Authorization: Bearer ACCESS_TOKEN"
```

##### Example Response


### POST /businesses/{business_id}/partners/ 
Create a new business partner for given business.

##### Example Request
```JavaScript
curl https://myaccounting.pymlo.com/businesses/dd921fea/partners/ \
  -H "Authorization: Bearer ACCESS_TOKEN" \
  -H "Content-Type: application/json" \
  -X POST \
  -d {
    "name": "Susan",
    "email": "susan@gmail.com",
    "customer": true
  }
```
##### Example Response


### PUT /businesses/{business_id}/partners/
Update an existing business partner. Please upload **whole partner data** includeing unmodified fields.

##### Example Request
```JavaScript
curl https://myaccounting.pymlo.com/businesses/dd921fea/partners/ \
  -H "Authorization: Bearer ACCESS_TOKEN" \
  -H "Content-Type: application/json" \
  -X POST \
  -d {
    "id": "bef8",
    "name": "Susan",
    "email": "susan@gmail.com",
    "customer": true
 }
```

##### Example Response


### DELETE /businesses/{business_id}/partners/{partner_id}/
Delete a business partner.

##### Example Request
```JavaScript
curl https://myaccounting.pymlo.com/businesses/dd921fea/partners/bef8/ \
  -H "Authorization: Bearer ACCESS_TOKEN"
  -X DELETE
```

##### Example Response

