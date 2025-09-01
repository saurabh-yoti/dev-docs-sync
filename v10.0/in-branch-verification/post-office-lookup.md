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
  "search_string": "EC3A 4AF"
}
{% /tab %}
{% /code %}

{% table widths="" %}
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
      "type": "UK_POST_OFFICE",
      "fad_code": "0040037",
      "name": "Houndsditch",
      "address": "11 White Kennet Street, London, Greater London",
      "post_code": "E1 7BS",
      "location": {
        "latitude": 51.5155,
        "longitude": -0.07693
      }
    },
    {
      "type": "UK_POST_OFFICE",
      "fad_code": "1010034",
      "name": "Moorgate",
      "address": "45 London Wall, London, Greater London",
      "post_code": "EC2M 5TE",
      "location": {
        "latitude": 51.51706,
        "longitude": -0.08797
      }
    }
  ]
}
{% /tab %}
{% /code %}

You will need the "fad_code" when creating the customer letter.

---

#### Error Codes

If the request is unsuccessful you will receive one of the below error responses in the form:

{% code %}
{% tab language="json" %}
{
    "code": "PAYLOAD_VALIDATION",
    "message": "There were errors validating the payload",
    "errors": [
        {
            "property": "search_string",
            "message": "must not be blank"
        }
    ]
}
{% /tab %}
{% /code %}

{% table widths="" %}
| Error code | Description | 
| ---- | ---- | 
| 400 | Payload validation error | 
{% /table %}