---
type: page
title: Post Office Lookup
listed: true
slug: post-office-lookup
description: 
index_title: Post Office Lookup
hidden: 
keywords: 
tags: 
---

The  following API endpoint can be used to locate Post Office branches closest to a supplied postcode, that can provide the In-Branch Verification (IBV) service. After the user has selected their preferred Post Office branch within your UI, the details of this branch can then be used to create the instructions for a In-Branch Verification request.

#### Endpoint

{% code %}
{% tab language="http" %}
POST https://api.yoti.com/idverify/v1/lookup/uk-post-office
{% /tab %}
{% /code %}

---

#### Request Body

{% code %}
{% tab language="json" %}
{
  "search_string": "HA5 2QW"
}
{% /tab %}
{% /code %}

{% table %}
| Parameter | Description | 
| ---- | ---- | 
| searchString | The searchString accepts a postcode, and will return the 10 nearest branches. | 
{% /table %}

---

#### Response Body

If the request is successful, the API will send a response in the form:

{% code %}
{% tab language="json" %}
{
  "branches": [
    {
      "type": "UK_POST_OFFICE"
      "fad_code": "12345678",
      "name": "St Neots",
      "address": "35 High Street, St. Neots, Cambridgeshire",
      "postcode": "PE19 1NL",
      "location": {
        "latitude": 52.22864,
        "longitude": -0.26762
      }
    }
  ]
}
{% /tab %}
{% /code %}

You will need the "fad_code" when creating the customer letter.