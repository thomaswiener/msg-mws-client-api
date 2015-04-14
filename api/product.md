---
layout: page
categories: ["API"]
title: Product
---

# Product

All API requests to `{{ site.vaola.api }}/product` require __HTTPS__.

The Products endpoint ... description

## Update product stock

The Stock endpoint allows you to update inventory quantities (stock levels) for an item.

> __Request__

```sh
curl -X PUT {{ site.vaola.api }}/product/ASUSUVNA1/stock \
    -d SKU=ASUSUVNA1 \
    -d Quantity=8 \
    -d Country=de
```

> __Response__ | 200 OK (JSON)

```
{
  "FeedSubmissionId": "50020016511",
  "FeedType": "_POST_INVENTORY_AVAILABILITY_DATA_",
  "SubmittedDate": {
    "date": "2015-03-17 13:54:23.000000",
    "timezone_type": 1,
    "timezone": "+00:00"
  },
  "FeedProcessingStatus": "_SUBMITTED_",
  "StartedProcessingDate": "",
  "CompletedProcessingDate": ""
}

```

### HTTP Request

`PUT {{ site.vaola.api }}/product/{SKU}/stock`

### Parameters

Parameter              | Description
---                    | ---
`SKU`                  | _VARCHAR_ - Used to identify an individual product. Each product must have a SKU, and each SKU must be unique. __Required__
`Country`              | _VARCHAR_ - ISO 639: 2-letter codes __Required__
`Quantity`             | _INTEGER_ - Indicates whether or not an item is available (any positive number = available; 0 = not available). Every time a quantity is sent for an item, the existing quantity is replaced by the new quantity in the feed. __Required , if Available is not set__
`Available`            | _BOOLEAN_ - Indicates whether or not the item is available (true = available; false = not available). __Required, if Quantity is not set__
`FulfillmentCenterID`  | _VARCHAR_ - Seller-defined identifier for a fulfillment center __Optional__
`FulfillmentLatency`   | _INTEGER_ - The number of days between the order date and the ship date (a whole number between 1 and 30). __Optional__
`RestockDate`          | _DATE_    - Date the item will be restocked, if not currently available __Optional__
`SwitchFulfillmentTo`  | _VARCHAR_ - Used only when switching the fulfillment of an item from MFN (merchant fulfilled) to AFN (Amazon fulfilled) or vice versa. __Optional__

### Response

Parameter                | Description
---                      | ---
`FeedSubmissionId`        | _String_   - A unique identifier for the feed submission.
`FeedType`                | _String_   - The type of feed submitted. This is the FeedType value that was provided to the SubmitFeed operation.
`SubmittedDate`           | _DateTime_ - The date and time when the feed was submitted.
`FeedProcessingStatus`    | _String_   - The processing status of the feed submission.
`StartedProcessingDate`   | _DateTime_ - The date when the feed processing started.
`CompletedProcessingDate` | _DateTime_ - The date when the feed processing completed.






## Update product price

The Price endpoint feed allows you to set the current price and sale price (when applicable) for an item. The sale price is optional, but, if used, the start and end date must be provided also.

> __Request__

```sh
curl -X PUT {{ site.vaola.api }}/product/ASUSUVNA1/price \
    -d SKU=ASUSUVNA1 \
    -d Country=de \
    -d StandardPrice=204.99 \
    -d Currency=EUR \
    -d StartDate=2008-10-01T00:00:00Z \
    -d EndDate=2009-01-31T00:00:00Z \
    -d SalePrice=28.38
```

> __Response__ | 200 OK (JSON)

```
{
  "FeedSubmissionId": "50020016511",
  "FeedType": "_POST_INVENTORY_AVAILABILITY_DATA_",
  "SubmittedDate": {
    "date": "2015-03-17 13:54:23.000000",
    "timezone_type": 1,
    "timezone": "+00:00"
  },
  "FeedProcessingStatus": "_SUBMITTED_",
  "StartedProcessingDate": "",
  "CompletedProcessingDate": ""
}
```

### HTTP Request

`PUT {{ site.vaola.api }}/product/{SKU}/price`

### Parameters

Parameter        | Description
---              | ---
`SKU`            | _VARCHAR_     - Used to identify an individual product. Each product must have a SKU, and each SKU must be unique. __Required__
`Country`        | _VARCHAR_     - ISO 639: 2-letter codes __Required__
`StandardPrice`  | _FLOAT_       - Price of the item (non-sale price) __Required__
`Currency`       | _VARCHAR(3)_  - Currency code as specified by [ISO4217](http://de.wikipedia.org/wiki/ISO_4217) __Required__
`StartDate`      | _DATETIME(c)_ - The date the sale starts (Sale Group) __Optional__
`EndDate`        | _DATETIME(c)_ - The last date of the sale (Sale Group) __Optional__
`SalePrice`      | _FLOAT_       - The sale price __Optional__
`MAP`            | _VARCHAR_     - Minimum Advertised Price. Use only if dictated by the manufacturer. Both the standard and sale price (if applicable) must be higher than the MAP value. __Not used for merchant accounts in Canada, Europe or Japan.__

### Response

Parameter               | Description
---                     | ---
`FeedSubmissionId`        | _String_   - A unique identifier for the feed submission.
`FeedType`                | _String_   - The type of feed submitted. This is the FeedType value that was provided to the SubmitFeed operation.
`SubmittedDate`           | _DateTime_ - The date and time when the feed was submitted.
`FeedProcessingStatus`    | _String_   - The processing status of the feed submission.
`StartedProcessingDate`   | _DateTime_ - The date when the feed processing started.
`CompletedProcessingDate` | _DateTime_ - The date when the feed processing completed.


