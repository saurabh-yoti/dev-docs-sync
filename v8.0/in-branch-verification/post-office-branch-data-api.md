---
type: page
title: Post Office Branch Data API
listed: false
slug: post-office-branch-data-api
description: 
index_title: Post Office Branch Data API
hidden: 
keywords: 
tags: 
---

The Post Office Location & Data Services (‘Branch Finder’) API can be used to locate Post Office branches closest to a supplied town or postcode, that can provide the In-Branch Verification (IBV) service.
After the user has selected their preferred Post Office branch within your UI, the details of this branch can then be used to create the instructions for a In-Branch Verification request.

#### Endpoint

{% code %}
{% tab language="http" %}
POST https://locations.pol-platform.co.uk/v1/locations/search
{% /tab %}
{% /code %}

---

#### Request Body

{% code %}
{% tab language="json" %}
{
   "searchString": "postcode",
   "productFilter": ["50321"]
}
{% /tab %}
{% /code %}

{% table widths="151" %}
| Parameter | Description | 
| ---- | ---- | 
| searchString | The searchString accepts a postcode, and will return the 10 nearest branches. | 
| productFilter | Filters out Post Office branches by products they support. “50321” is the code for In-Branch Verification. | 
{% /table %}

---

#### Response Body

If the request is successful, the API will send a response in the form:

{% code %}
{% tab language="json" %}
{
   "locationBusinessId": "123456X",
   "name": "Test Branch 1",
   "address": {
       "address1": "Address",
       "address2": "Address",
       "address3": "Address",
       "address4": "Town",
       "address5": "City",
       "postcode": "A1 1AA",
       "latitude": 51.51758,
       "longitude": -0.089212
   },
   "restrictedAccess": false,
   "tradingStatus": "trading",
   "coreHours": {
       "Monday": {
           "isOpen": true,
           "openTime": "09:00",
           "lunchCloseTime": "13:00",
           "lunchOpenTime": "14:00",
           "closeTime": "17:30"
       },
       "Tuesday": {
           "isOpen": true,
           "openTime": "09:00",
           "lunchCloseTime": "13:00",
           "lunchOpenTime": "14:00",
           "closeTime": "17:30"
       },
       "Wednesday": {
           "isOpen": true,
           "openTime": "09:00",
           "lunchCloseTime": "13:00",
           "lunchOpenTime": "14:00",
           "closeTime": "17:30"
       },
       "Thursday": {
           "isOpen": true,
           "openTime": "09:00",
           "lunchCloseTime": "13:00",
           "lunchOpenTime": "14:00",
           "closeTime": "17:30"
       },
       "Friday": {
           "isOpen": true,
           "openTime": "09:00",
           "lunchCloseTime": "13:00",
           "lunchOpenTime": "14:00",
           "closeTime": "17:30"
       },
       "Saturday": {
           "isOpen": true,
           "openTime": "09:00",
           "lunchCloseTime": "13:00",
           "lunchOpenTime": "14:00",
           "closeTime": "17:30"
       },
       "Sunday": {
           "isOpen": true,
           "openTime": "09:00",
           "lunchCloseTime": "13:00",
           "lunchOpenTime": "14:00",
           "closeTime": "17:30"
       }
   },
   "nextSevenDays": {
       "Monday": {
           "date": "2021-06-21",
           "isOpen": true,
           "openTime": "09:00",
           "lunchCloseTime": "13:00",
           "lunchOpenTime": "14:00",
           "closeTime": "17:30"
       },
       "Tuesday": {
           "date": "2021-06-22",
           "isOpen": true,
           "openTime": "09:00",
           "lunchCloseTime": "13:00",
           "lunchOpenTime": "14:00",
           "closeTime": "17:30"
       },
       "Wednesday": {
           "date": "2021-06-23",
           "isOpen": true,
           "openTime": "09:00",
           "lunchCloseTime": "13:00",
           "lunchOpenTime": "14:00",
           "closeTime": "17:30"
       },
       "Thursday": {
           "date": "2021-06-24",
           "isOpen": true,
           "openTime": "09:00",
           "lunchCloseTime": "13:00",
           "lunchOpenTime": "14:00",
           "closeTime": "17:30"
       },
       "Friday": {
           "date": "2021-06-25",
           "isOpen": true,
           "openTime": "09:00",
           "lunchCloseTime": "13:00",
           "lunchOpenTime": "14:00",
           "closeTime": "17:30"
       },
       "Saturday": {
           "date": "2021-06-26",
           "isOpen": true,
           "openTime": "09:00",
           "lunchCloseTime": "13:00",
           "lunchOpenTime": "14:00",
           "closeTime": "17:30"
       },
       "Sunday": {
           "date": "2021-06-27",
           "isOpen": true,
           "openTime": "09:00",
           "lunchCloseTime": "13:00",
           "lunchOpenTime": "14:00",
           "closeTime": "17:30"
       }
   },
   "Products": ["50321"],
   "siteMapURL": "https://www.postoffice.co.uk/branch-finder/123456X/test-branch-1",
   "comments": "lorem ipsum"
}
{% /tab %}
{% /code %}