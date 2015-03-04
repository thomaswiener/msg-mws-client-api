---
layout: page
categories: ["API"]
title: Product
---

# Product

All API requests to `{{ site.vaola.api }}/product` require __HTTPS__.

The Product endpoint ... description

## Update product stock

The Stock endpoint allows you to update inventory quantities (stock levels) for an item.

> Request

```sh
curl -X PUT {{ site.vaola.api }}/product/ASUSUVNA1/stock \
    -d MerchantIdentifier='M_SELLER_354577' \
    -d SKU=ASUSUVNA1 \
    -d Quantity=8 \
    -d FulFillmentLatency=1
```

> Response

```
200 OK
```

### HTTP Request

`PUT {{ site.vaola.api }}/product/stock`

### Parameters

Parameter              | Description
---                    | ---
`SKU`                  | _VARCHAR_ - Used to identify an individual product. Each product must have a SKU, and each SKU must be unique. __Required__
`MerchantIdentifier`   | _VARCHAR_ - Amazon Merchant Identifier __Required__
`FulfillmentCenterID`  | _VARCHAR_ - Seller-defined identifier for a fulfillment center
`Available`            | _BOOLEAN_ - Indicates whether or not the item is available (true = available; false = not available). __Required, if Quantity is not set__
`Quantity`             | _INTEGER_ - Indicates whether or not an item is available (any positive number = available; 0 = not available). Every time a quantity is sent for an item, the existing quantity is replaced by the new quantity in the feed. __Required , if Available is not set__
`FulfillmentLatency`   | _INTEGER_ - The number of days between the order date and the ship date (a whole number between 1 and 30). __Optional__
`RestockDate`          | _DATE_    - Date the item will be restocked, if not currently available __Optional__
`SwitchFulfillmentTo`  | _VARCHAR_ - Used only when switching the fulfillment of an item from MFN (merchant fulfilled) to AFN (Amazon fulfilled) or vice versa. __Optional__

__INTERNAL__

The request xml can be validated by the following XSD: [Inventory](https://images-na.ssl-images-amazon.com/images/G/01/rainier/help/xsd/release_1_9/Inventory.xsd)

### Response

Parameter       | Description
---             | ---
TBD             | TBD






## Update product price

The Price endpoint feed allows you to set the current price and sale price (when applicable) for an item. The sale price is optional, but, if used, the start and end date must be provided also.

> Request

```sh
curl -X PUT {{ site.vaola.api }}/product/price \
    -d MerchantIdentifier=M_SELLER_354577 \
    -d SKU=ASUSUVNA1 \
    -d StandardPrice=204.99 \
    -d Currency=EUR \
    -d StartDate=2008-10-01T00:00:00Z \
    -d EndDate=2009-01-31T00:00:00Z \
    -d SalePrice=28.38
```

> Response

```
200 OK
```

### HTTP Request

`PUT {{ site.vaola.api }}/product/price`

### Parameters

Parameter        | Description
---              | ---
`SKU`            | _VARCHAR_     - Used to identify an individual product. Each product must have a SKU, and each SKU must be unique. __Required__
`StandardPrice`  | _FLOAT_       - Price of the item (non-sale price) __Required__
`Currency`       | _VARCHAR(3)_  - Currency code as specified by [ISO4217](http://de.wikipedia.org/wiki/ISO_4217) __Required__
`StartDate`      | _DATETIME(c)_ - The date the sale starts __Optional__
`EndDate`        | _DATETIME(c)_ - The last date of the sale __Optional__
`SalePrice`      | _FLOAT_       - The sale price __Optional__
`MAP`            | _VARCHAR_     - Minimum Advertised Price. Use only if dictated by the manufacturer. Both the standard and sale price (if applicable) must be higher than the MAP value. __Not used for merchant accounts in Canada, Europe or Japan.__

__INTERNAL__

The request xml can be validated by the following XSD: [Price](https://images-na.ssl-images-amazon.com/images/G/01/rainier/help/xsd/release_1_9/Price.xsd)

### Response

Parameter       | Description
---             | ---
TBD             | TBD


