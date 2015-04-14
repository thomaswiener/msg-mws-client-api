---
layout: page
categories: ["API"]
title: Report
---

# Report

All API requests to `{{ site.vaola.api }}/report` require __HTTPS__.

This page contains the API enpoint definition of all functions needed to process an order/orderitem in Amazon Marketplace.

## Update Acknowledgement

The UpdateReportAcknowledgements operation is an optional request that updates the acknowledged status of one or more
reports. Use this operation if you want Amazon MWS to remember the acknowledged status of your reports. To keep track
of which reports you have already received, it is a good practice to acknowledge reports after you have received and
stored them successfully. Then, when you submit a GetReportList request, you can specify to receive only reports that
have not yet been acknowledged.

> Request


```sh
$ curl -X GET {{ site.bringmeister.api }}/report/updateacknowledgement
```

> Response

```
TBD
```

### HTTP Request

`GET {{ site.bringmeister.api }}/report/updateacknowledgement`


### Parameters

Parameter               | Description
---                     | ---
`Country`               | _String_  - ISO 639: 2-letter codes __Required__
`ReportId`              | _String_  - A structured list of Report Ids. The maximum number of reports that can be specified is 100.
`Acknowledged`          | _Boolean_ - A Boolean value that indicates that you have received and stored a report. Specify true to set the acknowledged status of a report to true. Specify false to set the acknowledged status of a report to false.

### Response

JSON as defined in http://docs.developer.amazonservices.com/en_DE/reports/Reports_UpdateReportAcknowledgements.html



