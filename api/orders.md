---
layout: page
categories: ["API"]
title: Orders
---

# Orders

All API requests to `{{ site.bringmeister.api }}/orders` require __HTTPS__.

lorem ipsum

## Retrieve a collection of orders

Order retrieve definition by Amazon


```sh
$ curl {{ site.bringmeister.api }}/slot/005c4826-4e28-11e3-a675-d43d7eece53d/12345
```

> Response

```json
{
  "id": "005c4826-4e28-11e3-a675-d43d7eece53d",
  "delivery_zone": "1",
  "store_no": "1234567",
  "price": "4.44",
  "currency": "EUR",
  "from": "{{ site.time | date: '%Y-%m-%d' }}T16:00:00{{ site.time | date: '%z' }}",
  "to": "{{ site.time | date: '%Y-%m-%d' }}T18:00:00{{ site.time | date: '%z' }}"
}
```

### HTTP Request

`GET {{ site.bringmeister.api }}/orders`


### Parameters

Parameter       | Description
---             | ---
`param1    `    | Definition __Required.__
`param2`        | Definition __Required.__








## Acknowledge an Order

Acknowledge an order


```sh
$ curl {{ site.vaola.api }}/orders/123456/acknowledge \
    -d slot_id=005c4826-4e28-11e3-a675-d43d7eece53d \
    --data-urlencode zip="012345"
```

> Response

```
201 CREATED
```

```json
{
  "id": "005c4826-4e28-11e3-a675-d43d7eece53d",
  "store_no": "1234567",
  "price": "4.44",
  "currency": "EUR",
  "from": "{{ site.time | date: '%Y-%m-%d' }}T16:00:00{{ site.time | date: '%z' }}",
  "to": "{{ site.time | date: '%Y-%m-%d' }}T18:00:00{{ site.time | date: '%z' }}"
}
```

### HTTP Request

`POST {{ site.vaola.api }}/orders/{orderId}/acknowledge`

### Parameters

Parameter      | Description
---            | ---
`param1`       | Description __Required.__
`param2`       | Description __Required.__





## Adjust an Order

lorem ipsum


```sh
$ curl {{ site.vaola.api }}/orders/123456/acknowledge \
    -d slot_id=005c4826-4e28-11e3-a675-d43d7eece53d \
    --data-urlencode zip="012345"
```

> Response

```
201 CREATED
```

```json
{
  "id": "005c4826-4e28-11e3-a675-d43d7eece53d",
  "store_no": "1234567",
  "price": "4.44",
  "currency": "EUR",
  "from": "{{ site.time | date: '%Y-%m-%d' }}T16:00:00{{ site.time | date: '%z' }}",
  "to": "{{ site.time | date: '%Y-%m-%d' }}T18:00:00{{ site.time | date: '%z' }}"
}
```

### HTTP Request

`POST {{ site.vaola.api }}/orders/{orderId}/acknowledge`

### Parameters

Parameter      | Description
---            | ---
`param1`       | Description __Required.__
`param2`       | Description __Required.__


