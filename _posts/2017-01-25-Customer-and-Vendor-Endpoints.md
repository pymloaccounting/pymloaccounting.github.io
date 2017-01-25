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
where other fields are optional.

## Overview
| Endpoint                                                        |  Description  |
| -------------                                                   | ----- |
| [GET /businesses/{business_id}/partners/](#get-businessesbusiness_idpartners)  | Get a list of business partners from given business |
| [GET /businesses/{business_id}/partners/{partner_id}/](#get-businessesbusiness_idpartnerspartner_id) |  Get a specific business partner |
| [POST /businesses/{business_id}/partner/](#post-businessesbusiness_idpartner) |  Create a new business partner for given business |
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
| sell                              | boolean       | True if you sell product to a partner.        |
| buy                               | boolean       | True if you buy product from a partner.       |
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
curl https://myaccounting.pymlo.com/businesses/dd921fea-bef8-4281-a400-abefe265b601/partners/ \
  -H "Authorization: Bearer ACCESS_TOKEN"
  
##### Example Response


### GET /businesses/{business_id}/partners/{partner_id}/

### POST /businesses/{business_id}/partner/ 

### PUT /businesses/{business_id}/partners/

### DELETE /businesses/{business_id}/partners/{partner_id}/



### In erat ligula

In auctor tellus eu metus pellentesque, quis facilisis nibh placerat. Commodo in lorem eget, vulputate bibendum ante. Etiam vestibulum quis diam a dapibus. Integer fermentum nec purus sed dictum. Donec fermentum et sapien eget suscipit. Fusce consequat est a ex molestie ultrices.

<img src="http://placehold.it/800x600">

## Section 2

Donec dictum hendrerit rutrum: 

> Proin ultrices hendrerit vestibulum. Curabitur non placerat metus. Donec suscipit ligula et aliquam semper. Fusce sed imperdiet augue. Suspendisse potenti. Cras vestibulum, metus et vulputate ornare, ante libero gravida felis, a bibendum magna felis ut tortor.

<img src="http://placehold.it/800x600">

## Section 3

Sed molestie augue libero, eget suscipit velit euismod ullamcorper.

`fibonacci.js`:

```javascript
var Fib = {
    [Symbol.iterator]() {
        var n1 = 1, n2 = 1;

        return {
            // make the iterator an iterable
            [Symbol.iterator]() { return this; },

            next() {
                var current = n2;
                n2 = n1;
                n1 = n1 + current;
                return { value: current, done: false };
            },

            return(v) {
                console.log(
                    "Fibonacci sequence abandoned."
                );
                return { value: v, done: true };
            }
        };
    }
};

for (var v of Fib) {
    console.log( v );

    if (v > 50) break;
}
// 1 1 2 3 5 8 13 21 34 55
// Fibonacci sequence abandoned.
```

## Section 4

### Pellentesque lobortis volutpat maximus 

Etiam condimentum:

- orci non consequat elementum
- tortor tellus viverra neque
- id dignissim nibh nisl id magna
- suspendisse aliquet dolor vehicula velit imperdiet

Suspendisse pretium molestie metus a consectetur. Sed nec interdum magna. Suspendisse efficitur, mi eget finibus mollis, orci tortor dignissim nisi, non vestibulum velit tellus ut odio. Praesent vitae sapien varius, mollis nunc vel, interdum nunc.

<img src="http://placehold.it/800x600">
