---
layout: page
categories: ["API"]
title: Order
---

# Order

All API requests to `{{ site.vaola.api }}/orders` require __HTTPS__.

This page contains the API enpoint definition of all functions needed to process an order/orderitem in Amazon Marketplace.

## Retrieve a collection of orders

You retrieve the Order Report, which contains a list of new orders received after the previous Order Report was
created. This report contains all of the information you need for processing your orders.

> Request


```sh
$ curl -X GET {{ site.bringmeister.api }}/orders
```

> Response

```
TBD
```

### HTTP Request

`GET {{ site.bringmeister.api }}/orders`


### Parameters

Parameter               | Description
---                     | ---
`MerchantIdentifier`    | _VARCHAR_ - Amazon Merchant Identifier __Required__








## Acknowledge an Order(Item)

The Order Acknowledgment endpoint allows you to acknowledge your success or failure with downloading an order.
The acknowledgment also allows you to provide your own order ID and order item IDs, which you can then reference
in future feeds for the same order, if desired.

Additionally, you can use this feed to cancel the entire order under one of these circumstances:

* The customer asked you to cancel the order (and you have not yet shipped it)
* You received a single-item order but you can't ship the item (damaged goods)
* You are unable to upload an order into your system

To cancel the order, use the "Failure" StatusCode.

__DEV REMARKS__

Every item on an order needs an acknowledgment. How do we define the api for several order items? Or do we acknowledge all items step by step?

> Request

```sh
curl -X POST {{ site.vaola.api }}/order/acknowledgement \
    -d MerchantIdentifier='M_SELLER_354577' \
    -d AmazonOrderID=050-1234567-1234567 \
    -d MerchantOrderID=12345678 \
    -d StatusCode=Success
    -d AmazonOrderItemCode=1234567890
    -d MerchantOrderItemID=1234567
```

> Response

```
200 OK
```

### HTTP Request

`POST {{ site.vaola.api }}/order/acknowledgement`

### Parameters

Parameter             | Description
---                   | ---
`MerchantIdentifier`  | _VARCHAR_ - Amazon Merchant Identifier __Required__
`AmazonOrderID`       | _VARCHAR_ - Amazon's unique identifier for an order, which identifies the entire order regardless of the number of individual items in the order __Required__
`MerchantOrderID`     | _VARCHAR_ - Seller-supplied order ID, will be mapped by Amazon to the AmazonOrderID, can be used for reference __Optional__
`StatusCode`          | _VARCHAR_ - Allows you to acknowledge your success or failure with downloading an order. StatusCode can be either "Success" or "Failure." A StatusCode of "Failure" can be used for communicating to Amazon that you had a problem integrating the order into your system and are unable to process the order. Sending status code "Failure" will automatically cancel the order; the customer will not be charged for the item. __Required.__
`AmazonOrderItemCode` | _VARCHAR_ - Amazon's unique identifier for an item in an order. If the MerchantOrderItemID is also specified, Amazon will map the two IDs and you can then use your own item ID for subsequent feeds relating to that item within the order. __Required.__
`MerchantOrderItemID` | _VARCHAR_ - Seller-supplied ID for an item in an order. __Optional__
`CancelReason`        | _VARCHAR_ - Used only when sending a StatusCode of "Failure." __Required__

__INTERNAL__

The request xml can be validated by the following XSD: [OrderAcknowledgement](https://images-na.ssl-images-amazon.com/images/G/01/rainier/help/xsd/release_1_9/OrderAcknowledgement.xsd)




## Ship an Order(Item)

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
    -d MerchantIdentifier='M_SELLER_354577' \
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

Parameter                   | Description
---                         | ---
`MerchantIdentifier`        | _VARCHAR_ - Amazon Merchant Identifier __Required__
`AmazonOrderID`             | _VARCHAR_ - Amazon's unique identifier for an order, which identifies the entire order regardless of the number of individual items in the order __Required__
`MerchantOrderID`           | _VARCHAR_ - Seller-supplied order ID, will be mapped by Amazon to the AmazonOrderID, can be used for reference __Optional__
`MerchantFulfillmentID`     | _VARCHAR_ - Allows you to acknowledge your success or failure with downloading an order. StatusCode can be either "Success" or "Failure." A StatusCode of "Failure" can be used for communicating to Amazon that you had a problem integrating the order into your system and are unable to process the order. Sending status code "Failure" will automatically cancel the order; the customer will not be charged for the item. __Required.__
`FulfillmentDate`           | _VARCHAR_ - Amazon's unique identifier for an item in an order. If the MerchantOrderItemID is also specified, Amazon will map the two IDs and you can then use your own item ID for subsequent feeds relating to that item within the order. __Required.__
`CarrierCode`               | _VARCHAR_ - Shipping carrier code __Optional__
`CarrierName`               | _VARCHAR_ - Shipping carrier name __Optional__
`ShippingMethod`            | _VARCHAR_ - Shipping method used to deliver the item __Optional__
`ShipperTrackingNumber`     | _VARCHAR_ - Tracking number for the shipment __Optional__
`AmazonOrderItemCode`       | _VARCHAR_ - Amazon's unique identifier for an item in an order. __Required__
`MerchantOrderItemID`       | _VARCHAR_ - Seller-supplied ID for an item in an order. __Optional__
`MerchantFulfillmentItemID` | _VARCHAR_ - Seller-supplied unique identifier for an item in the shipment (not used by Amazon) __Required__
`Quantity`                  | _INTEGER_ - The quantity shipped (if more than one of a given item was purchased, and all of them are not shipped together) __Required__

__INTERNAL__

The request xml can be validated by the following XSD: [OrderFulfillment](https://images-na.ssl-images-amazon.com/images/G/01/rainier/help/xsd/release_1_9/OrderFulfillment.xsd)






## Adjust an Order(Item)

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
    -d MerchantIdentifier='M_SELLER_354577' \
    -d AmazonOrderID=050-1234567-1234567 \
    -d MerchantOrderItemID=123456789 \
    -d MerchantAdjustmentItemID=12345 \
    -d AdjustmentReason=Success \
    -d ItemPriceAdjustments=10.23 \
    -d Currency=2
```

> Response

```
200 OK
```

### HTTP Request

`POST {{ site.vaola.api }}/order/adjustment`

### Parameters

Parameter                   | Description
---                         | ---
`MerchantIdentifier`        | _VARCHAR_ - Amazon Merchant Identifier __Required__
`AmazonOrderID`             | _VARCHAR_ - Amazon's unique identifier for an order, which identifies the entire order regardless of the number of individual items in the order __Required__
`MerchantOrderID`           | _VARCHAR_ - Seller-supplied order ID, will be mapped by Amazon to the AmazonOrderID, can be used for reference __Optional__
`AmazonOrderItemCode`       | _VARCHAR_ - Amazon's unique identifier for an item in an order. __Required__
`MerchantOrderItemID`       | _VARCHAR_ - Seller-supplied ID for an item in an order. __Optional__
`MerchantAdjustmentItemID`  | _VARCHAR_ - Optional seller-supplied unique ID for the adjustment (not used by Amazon) __Required__
`AdjustmentReason`          | _VARCHAR_ - Reason for the adjustment __Required.__
`ItemPriceAdjustments`      | _VARCHAR_ - Amounts the buyer is to be refunded for the item. __Required.__
`PromotionAdjustments`      | _VARCHAR_ - Amounts the buyer is to be refunded for a promotion. __Required.__
`QuantityCancelled`         | _INTEGER_ - Quantity of items being cancelled. Used only for partial cancellations. __Optional__
`Currency`                  | _VARCHAR(3)_ - Currency code as specified by [ISO4217](http://de.wikipedia.org/wiki/ISO_4217) __Required__

__INTERNAL__

The request xml can be validated by the following XSD: [OrderAdjustment](https://images-na.ssl-images-amazon.com/images/G/01/rainier/help/xsd/release_1_9/OrderAdjustment.xsd)

