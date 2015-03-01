---
layout: page
categories: ["API"]
title: Products
---

# Products

All API requests to `{{ site.vaola.api }}/product` require __HTTPS__.

The Product endpoint ... description

## Update product stock

Update the stock information of a single product

```sh
$ curl {{ site.vaola.api }}/products/12345/stock
```

> Response

```json
[{
  "id": "005c4826-4e28-11e3-a675-d43d7eece53d",
  "store_no":"2250274",
  "from": "{{ site.time | date: '%Y-%m-%d' }}T16:00:00{{ site.time | date: '%z' }}",
  "to": "{{ site.time | date: '%Y-%m-%d' }}T18:00:00{{ site.time | date: '%z' }}",
  "finish":"2014-06-07 09:45:00",
  "price":"5.55",
  "currency": "EUR",
  "capacity":"0",
  "working_shift":"1",
},
....
]
```

### HTTP Request

`PUT {{ site.vaola.api }}/products/{asin}/stock`

### Parameters

Parameter      | Description
---            | ---
`asin`          | VARCHAR(5) - Amazon Standard Identification Number (ASIN), the products' unique identification number

### Response

Parameter       | Description
---             | ---
`id`            | VARCHAR(32) - UUID, The Slot Id
`store_no`      | INT - The Store Id
`from`          | DATETIME - Time of Slot Start
`to`            | DATETIME - Time of Slot End
`finish`        | DATETIME - Final datetime until this slot can be booked
`price`         | DECIMAL(6,4) - The price of the slot
`currency`      | VARCHAR(3) - Currency as defined by [ISO 4217](http://de.wikipedia.org/wiki/ISO_4217)
`capacity`      | INT
`working_shift` | TBD

## Update product price

Update the price information of a single product

```sh
$ curl {{ site.vaola.api }}/products/12345/price
```

> Response

```json
[{
  "id": "005c4826-4e28-11e3-a675-d43d7eece53d",
  "store_no":"2250274",
  "from": "{{ site.time | date: '%Y-%m-%d' }}T16:00:00{{ site.time | date: '%z' }}",
  "to": "{{ site.time | date: '%Y-%m-%d' }}T18:00:00{{ site.time | date: '%z' }}",
  "finish":"2014-06-07 09:45:00",
  "price":"5.55",
  "currency": "EUR",
  "capacity":"0",
  "working_shift":"1",
},
....
]
```

### HTTP Request

`PUT {{ site.vaola.api }}/products/{asin}/price`

### Parameters

Parameter      | Description
---            | ---
`asin`          | VARCHAR(5) - Amazon Standard Identification Number (ASIN), the products' unique identification number

### Response

Parameter       | Description
---             | ---
`id`            | VARCHAR(32) - UUID, The Slot Id
`store_no`      | INT - The Store Id
`from`          | DATETIME - Time of Slot Start
`to`            | DATETIME - Time of Slot End
`finish`        | DATETIME - Final datetime until this slot can be booked
`price`         | DECIMAL(6,4) - The price of the slot
`currency`      | VARCHAR(3) - Currency as defined by [ISO 4217](http://de.wikipedia.org/wiki/ISO_4217)
`capacity`      | INT
`working_shift` | TBD
