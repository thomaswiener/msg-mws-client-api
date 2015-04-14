---
layout: page
categories: ["API"]
title: Order
---

# Order

All API requests to `{{ site.vaola.api }}/order` require __HTTPS__.

This page contains the API enpoint definition of all functions needed to process an order/orderitem in Amazon Marketplace.

## Retrieve a collection of orders

The ListOrders operation returns a list of orders created or updated during a time frame that you specify.
You define that time frame using the CreatedAfter parameter or the LastUpdatedAfter parameter.
You must use one of these parameters, but not both. You can also apply a range of filtering criteria to narrow
the list of orders that is returned. The ListOrders operation includes order information for each order returned,
including AmazonOrderId, OrderStatus, FulfillmentChannel, and LastUpdateDate.

> Request


```sh
$ curl -X GET {{ site.bringmeister.api }}/order
```

> Response | 200 OK (JSON)

```
{
  "ListOrderItemsResult": {
    "NextToken": "string",
    "AmazonOrderId": "string",
    "OrderItems": [
      {
        "ASIN": "123-1233123-1231321",
        "SellerSKU": "1266589",
        "OrderItemId": "12341234",
        "Title": "string",
        "QuantityOrdered": "1",
        "QuantityShipped": "0",
        "ItemPrice": {
          "CurrencyCode": "EUR",
          "Amount": "13.72"
        },
        "ShippingPrice": {
          "CurrencyCode": "EUR",
          "Amount": "2.77"
        },
        "GiftWrapPrice": {
          "CurrencyCode": "EUR",
          "Amount": "string"
        },
        "ItemTax": {
          "CurrencyCode": "EUR",
          "Amount": "1.11"
        },
        "ShippingTax": {
          "CurrencyCode": "EUR",
          "Amount": "0.45"
        },
        "GiftWrapTax": {
          "CurrencyCode": "EUR",
          "Amount": "0.34"
        },
        "ShippingDiscount": {
          "CurrencyCode": "EUR",
          "Amount": "0.00"
        },
        "PromotionDiscount": {
          "CurrencyCode": "EUR",
          "Amount": "0.00"
        },
        "PromotionIds": [
          "EUR"
        ],
        "CODFee": {
          "CurrencyCode": "EUR",
          "Amount": "0.00"
        },
        "CODFeeDiscount": {
          "CurrencyCode": "EUR",
          "Amount": "0.00"
        },
        "GiftMessageText": "Congrats to Whatever",
        "GiftWrapLevel": "1",
        "InvoiceData": {
          "InvoiceRequirement": "true",
          "BuyerSelectedInvoiceCategory": "true",
          "InvoiceTitle": "ACME Company",
          "InvoiceInformation": "Bla Bla"
        },
        "ConditionNote": null,
        "ConditionId": null,
        "ConditionSubtypeId": null,
        "ScheduledDeliveryStartDate": null,
        "ScheduledDeliveryEndDate": null
      },
      {
        "ASIN": "56456-456456-456465",
        "SellerSKU": "1266589",
        "OrderItemId": "12341234",
        "Title": "string",
        "QuantityOrdered": "2",
        "QuantityShipped": "0",
        "ItemPrice": {
          "CurrencyCode": "EUR",
          "Amount": "45.99"
        },
        "ShippingPrice": {
          "CurrencyCode": "EUR",
          "Amount": "5.92"
        },
        "GiftWrapPrice": {
          "CurrencyCode": "EUR",
          "Amount": "string"
        },
        "ItemTax": {
          "CurrencyCode": "EUR",
          "Amount": "1.11"
        },
        "ShippingTax": {
          "CurrencyCode": "EUR",
          "Amount": "0.45"
        },
        "GiftWrapTax": {
          "CurrencyCode": "EUR",
          "Amount": "0.34"
        },
        "ShippingDiscount": {
          "CurrencyCode": "EUR",
          "Amount": "0.00"
        },
        "PromotionDiscount": {
          "CurrencyCode": "EUR",
          "Amount": "0.00"
        },
        "PromotionIds": [
          "EUR"
        ],
        "CODFee": {
          "CurrencyCode": "EUR",
          "Amount": "0.00"
        },
        "CODFeeDiscount": {
          "CurrencyCode": "EUR",
          "Amount": "0.00"
        },
        "GiftMessageText": "Congrats to Whatever",
        "GiftWrapLevel": "1",
        "InvoiceData": {
          "InvoiceRequirement": "true",
          "BuyerSelectedInvoiceCategory": "true",
          "InvoiceTitle": "ACME Company",
          "InvoiceInformation": "Bla Bla"
        },
        "ConditionNote": null,
        "ConditionId": null,
        "ConditionSubtypeId": null,
        "ScheduledDeliveryStartDate": null,
        "ScheduledDeliveryEndDate": null
      }
    ]
  },
  "ResponseMetadata": {
    "RequestId": "string"
  }
}
```

### HTTP Request

`GET {{ site.bringmeister.api }}/order`


### Parameters

Parameter               | Description
---                     | ---
CreatedAfter            | _DateTime_ - A date used for selecting orders created after (or at) a specified time, in ISO 8601 date format. __Required (if LastUpdatedAfter is not specified)__
CreatedBefore           | _DateTime_ - A date used for selecting orders created before (or at) a specified time, in ISO 8601 date format. __Optional__ (Only if CreatedAfter is specified)
LastUpdatedAfter        | _DateTime_ - A date used for selecting orders that were last updated after (or at) a specified time, in ISO 8601 date format. An update is defined as any change in order status, including the creation of a new order. Includes updates made by Amazon and by the seller. __Required (if CreatedAfter is not specified)__
LastUpdatedBefore       | _DateTime_ - A date used for selecting orders that were last updated before (or at) a specified time, in ISO 8601 date format. An update is defined as any change in order status, including the creation of a new order. Includes updates made by Amazon and by the seller. __Optional__ (Only if LastUpdatedAfter is specified)
OrderStatus             | _String_   - A list of OrderStatus values. Used to select orders with a current status that matches one of the status values that you specify. __Optional__
FulfillmentChannel      | _String_   - A list that indicates how an order was fulfilled. __Optional__
PaymentMethod           | _String_   - A list of PaymentMethod values. Used to select orders paid for with the payment methods that you specify. __Optional__
BuyerEmail              | _String_   - The e-mail address of a buyer. Used to select only the orders that contain the specified e-mail address. __Optional__
SellerOrderId           | _String_   - An order identifier that is specified by the seller. Not an Amazon order identifier. Used to select only the orders that match a seller-specified order identifier. __Optional__
MaxResultsPerPage       | _String_   - A number that indicates the maximum number of orders that can be returned per page. __Optional__
TFMShipmentStatus       | _String_   - A list of TFMShipmentStatus values. Used to select Amazon Transportation for Merchants (TFM) orders with a current status that matches one of the status values that you specify. __Optional__

### Response

JSON object as defined in http://docs.developer.amazonservices.com/en_DE/orders/2013-09-01/Orders_Datatypes.html#Order

__Amazon Docs__

For a full list of optional dependencies parameters and definitions see http://docs.developer.amazonservices.com/en_DE/orders/2013-09-01/Orders_ListOrders.html as the api has been adapted to the MWS API features.






## Retrieve a collection of orderitems

YThe ListOrderItems operation returns order item information for an AmazonOrderId that you specify.
The order item information includes Title, ASIN, SellerSKU, ItemPrice, ShippingPrice,
as well as tax and promotion information.

> Request


```sh
$ curl -X GET {{ site.bringmeister.api }}/order/item
```

> Response

```
TBD
```

### HTTP Request

`GET {{ site.bringmeister.api }}/order/item`


### Parameters

Parameter               | Description
---                     | ---
AmazonOrderId           | _String_ - An Amazon-defined order identifier, in 3-7-7 format. __Required__


### Response

JSON object as defined in http://docs.developer.amazonservices.com/en_DE/orders/2013-09-01/Orders_Datatypes.html#OrderItem





## Acknowledge an Order

The Order Acknowledgment endpoint allows you to acknowledge your success or failure with downloading an order.
The acknowledgment also allows you to provide your own order ID and order item IDs, which you can then reference
in future feeds for the same order, if desired.

Additionally, you can use this feed to cancel the entire order under one of these circumstances:

* The customer asked you to cancel the order (and you have not yet shipped it)
* You received a single-item order but you can't ship the item (damaged goods)
* You are unable to upload an order into your system

To cancel the order, use the "Failure" StatusCode.

> Request

```sh
curl -X POST {{ site.vaola.api }}/order/acknowledgement \
    -d AmazonOrderID=050-1234567-1234567 \
    -d MerchantOrderID=12345678 \
    -d StatusCode=Success
    -d AmazonOrderItemCode_1=1234567890
    -d MerchantOrderItemID_1=234567
```

> Response

```
200 OK
```

### HTTP Request

`POST {{ site.vaola.api }}/order/acknowledgement`

### Parameters

Parameter               | Description
---                     | ---
`AmazonOrderID`         | _VARCHAR_ - Amazon's unique identifier for an order, which identifies the entire order regardless of the number of individual items in the order __Required__
`MerchantOrderID`       | _VARCHAR_ - Seller-supplied order ID, will be mapped by Amazon to the AmazonOrderID, can be used for reference __Optional__
`StatusCode`            | _VARCHAR_ - Allows you to acknowledge your success or failure with downloading an order. StatusCode can be either "Success" or "Failure." A StatusCode of "Failure" can be used for communicating to Amazon that you had a problem integrating the order into your system and are unable to process the order. Sending status code "Failure" will automatically cancel the order; the customer will not be charged for the item. __Required.__
`AmazonOrderItemCode_X` | _VARCHAR_ - Amazon's unique identifier for an item in an order. If the MerchantOrderItemID is also specified, Amazon will map the two IDs and you can then use your own item ID for subsequent feeds relating to that item within the order. __Required.__
`MerchantOrderItemID_X` | _VARCHAR_ - Seller-supplied ID for an item in an order. __Optional__
`CancelReason`          | _VARCHAR_ - Used only when sending a StatusCode of "Failure." __Required__








## Ship an Order

The Order Fulfillment endpoint allows your system to update Amazon's system with order fulfillment information.
Amazon posts the information in the customer's Amazon account so the customer can check the shipment status.

Once you've shipped the order, send Amazon a shipping confirmation with fulfillment information.
If you shipped the order using a trackable shipping method, include the tracking number in the feed.
Amazon provides standard shipper codes (CarrierCode) as well as free-text fields so you can enter a different shipper.

This feed is important because it signals Amazon to charge the buyer, credit your Marketplace Payments account,
and notify the buyer that the order is on the way. If Amazon does not receive the confirmation within 30 days of the
order being placed, the order will be canceled automatically and you will not be paid for the order.

You can send your own unique order and item identifiers (MerchantOrderID and MerchantOrderItemID) rather than
Amazon's order and item identifiers, if you established your own in the OrderAcknowledgment feed.


> Request

```sh
curl -X POST {{ site.vaola.api }}/order/fulfillment \
    -d AmazonOrderID=050-1234567-1234567 \
    -d MerchantFulfillmentID=Success \
    -d FulfillmentDate=2008-10-01T00:00:00 \
    -d CarrierCode=UPS \
    -d ShippingMethod='Second Day' \
    -d ShipperTrackingNumber=123456789 \
    -d MerchantOrderItemID=123456789 \
    -d MerchantFulfillmentItemID=123456789 \
    -d Quantity=2
```

> Response

```
200 OK
```

### HTTP Request

`POST {{ site.vaola.api }}/order/fulfillment`

### Parameters

Parameter                     | Description
---                           | ---
`AmazonOrderID`               | _VARCHAR_ - Amazon's unique identifier for an order, which identifies the entire order regardless of the number of individual items in the order __Required__
`MerchantOrderID`             | _VARCHAR_ - Seller-supplied order ID, will be mapped by Amazon to the AmazonOrderID, can be used for reference __Optional__
`MerchantFulfillmentID`       | _VARCHAR_ - Allows you to acknowledge your success or failure with downloading an order. StatusCode can be either "Success" or "Failure." A StatusCode of "Failure" can be used for communicating to Amazon that you had a problem integrating the order into your system and are unable to process the order. Sending status code "Failure" will automatically cancel the order; the customer will not be charged for the item. __Required.__
`FulfillmentDate`             | _VARCHAR_ - Amazon's unique identifier for an item in an order. If the MerchantOrderItemID is also specified, Amazon will map the two IDs and you can then use your own item ID for subsequent feeds relating to that item within the order. __Required.__
`CarrierCode`                 | _VARCHAR_ - Shipping carrier code __Optional__
`CarrierName`                 | _VARCHAR_ - Shipping carrier name __Optional__
`ShippingMethod`              | _VARCHAR_ - Shipping method used to deliver the item __Optional__
`ShipperTrackingNumber`       | _VARCHAR_ - Tracking number for the shipment __Optional__
`AmazonOrderItemCode_X`       | _VARCHAR_ - Amazon's unique identifier for an item in an order. __Required__
`MerchantOrderItemID_X`       | _VARCHAR_ - Seller-supplied ID for an item in an order. __Optional__
`MerchantFulfillmentItemID_X` | _VARCHAR_ - Seller-supplied unique identifier for an item in the shipment (not used by Amazon) __Required__
`Quantity_X`                  | _INTEGER_ - The quantity shipped (if more than one of a given item was purchased, and all of them are not shipped together) __Required__









## Adjust an Order

The Order Adjustment endpoint allows you to issue a refund (adjustment) for an order.
You must provide a reason for the adjustment, such as "Customer Return," and the adjustment amount,
broken out by price component (principle, shipping, tax, and so on).
Note, however, that the buyer's credit card will only be credited one time for the total amount.
Although the adjustment feed allows for charging the buyer additional money (for a restocking fee, for
example), the net amount of the adjustment must be a credit to the buyer.

Additionally, you can use the Order Adjustment feed to cancel individual items that you are unable to ship, without
incurring a refund holdback fee. __To use this feature, you must provide an adjustment reason of NoInventory or
BuyerCancelled, and the quantity of items being cancelled.__


> Request

```sh
curl -X POST {{ site.vaola.api }}/order/adjustment \
    -d AmazonOrderID=050-1234567-1234567 \
    -d MerchantOrderItemID=123456789 \
    -d MerchantAdjustmentItemID=12345 \
    -d AdjustmentReason=Success \
    -d ItemPriceAdjustments=10.23 \
    -d Currency=EUR
```

> Response

```
200 OK
```

### HTTP Request

`POST {{ site.vaola.api }}/order/adjustment`

### Parameters

Parameter                     | Description
---                           | ---
`AmazonOrderID`               | _VARCHAR_ - Amazon's unique identifier for an order, which identifies the entire order regardless of the number of individual items in the order __Required__
`MerchantOrderID`             | _VARCHAR_ - Seller-supplied order ID, will be mapped by Amazon to the AmazonOrderID, can be used for reference __Optional__
`AmazonOrderItemCode_X`       | _VARCHAR_ - Amazon's unique identifier for an item in an order. __Required__
`MerchantOrderItemID_X`       | _VARCHAR_ - Seller-supplied ID for an item in an order. __Optional__
`MerchantAdjustmentItemID_X`  | _VARCHAR_ - Optional seller-supplied unique ID for the adjustment (not used by Amazon) __Required__
`AdjustmentReason`            | _VARCHAR_ - Reason for the adjustment __Required.__
`ItemPriceAdjustments`        | _VARCHAR_ - Amounts the buyer is to be refunded for the item. __Required.__
`PromotionAdjustments`        | _VARCHAR_ - Amounts the buyer is to be refunded for a promotion. __Required.__
`QuantityCancelled`           | _INTEGER_ - Quantity of items being cancelled. Used only for partial cancellations. __Optional__
`Currency`                    | _VARCHAR(3)_ - Currency code as specified by [ISO4217](http://de.wikipedia.org/wiki/ISO_4217) __Required__


