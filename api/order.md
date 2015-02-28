---
layout: page
categories: ["API"]
title: Slots
---

# Slots

All API requests to `{{ site.bringmeister.api }}/slot` require __HTTPS__.

A slot is a time period, defined by a date, begin time, and end time.
Not for all zip codes the same set of slots is available.
A slot, which is available for the zip code, can be reserved for the customer,
booked by the customer, and cancelled or released by the shop.

## Reserve a Slot

A slot is reserved for the customer when the customer selects the
desired delivery time. At this moment the checkout is not completed,
yet, but the customer has selected a delivery time already.


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

`GET {{ site.bringmeister.api }}/slot/{slot_id}/{zip}`


### Parameters

Parameter      | Description
---            | ---
`slot_id    `  | The id of the selected slot __Required.__
`zip`          | The zip code of selected slot  __Required.__


## Book a Slot

A slot is booked for the customer when the checkout is completed.
At this time the previously made reservation changes into a booking.


```sh
$ curl {{ site.bringmeister.api }}/slot \
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

`POST {{ site.bringmeister.api }}/slot`

### Parameters

Parameter      | Description
---            | ---
`slot_id    `  | The id of the selected slot __Required.__
`zip`          | The zip code of selected slot  __Required.__


## Cancel a Slot

A cancellation must be made when the customer cancels a
previously made booking. Only complete bookings can be cancelled.


```sh
$ curl {{ site.bringmeister.api }}/slot/005c4826-4e28-11e3-a675-d43d7eece53d
```

> Response

```
200 OK
```

### HTTP Request

`DELETE {{ site.bringmeister.api }}/slot/{slot_id}`

### Parameters

Parameter      | Description
---            | ---
`slot_id    `  | The id of the selected slot __Required.__


## Release a Slot

A slot which is reserved for a customer has to be released
after a fixed time period, if the customer did not complete
the checkout by then. If the customer does not complete the
checkout, the slot must be available again for new reservations.


```sh
$ curl {{ site.bringmeister.api }}/slot/005c4826-4e28-11e3-a675-d43d7eece53d/12345
```

> Response

```
200 OK
```

### HTTP Request

`PUT {{ site.bringmeister.api }}/slot/{slot_id}`

### Parameters

Parameter      | Description
---            | ---
`slot_id    `  | The id of the selected slot __Required.__
