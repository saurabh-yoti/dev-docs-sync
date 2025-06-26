---
type: page
title: Secure image capture
listed: true
slug: secure-image-capture
description: 
index_title: Secure image capture
hidden: 
keywords: 
tags: 
---

Yoti age estimation now supports the SICAP (Secure Image Capture) feature. This ensures the captured image has not been manipulated (for e.g., injection attacks) before it is submitted to the Yoti backend for processing. 

In order to use SICAP, you will need to:

- Upgrade to Yoti’s Face Capture Module (FCM) version 1.0.0 or later.
- Set the secure prop to true.
- Use the new FCM outputs "img" and "secure".
- Add a query parameter when calling the Yoti API endpoints.
- Modify the API request body with a "secure" output added.

{% html %}
<div class="alert-GTK">
    <div class="alert-title" id="GTK">
        Good to know
    </div>
    <div class="alert-text">
      FCM image output cannot be modified. Any change in ‘img’ will be rejected by the backend.
    </div>
    <div class="alert-links"> 

   </div>
</div>
{% /html %}

---

## Endpoints

If you wish to use the secure feature, you will need to add the query parameter ‘?secure=true’ to the applicable endpoint below:

- /v1/age?secure=true
- /v1/age-antispoofing?secure=true
- /v1/antispoofing?secure=true

**Note:** if secure is requested, you will also need to add a “secure” field in the request body, or you will get an **'INVALID_REQUEST_BODY'** error message.

If using the YotiSDK, the query parameter should be set with the appropriate query parameter function call, not directly to the endpoint.

## Request body

Face capture module will automatically return “img” and “secure” on success. Do not modify these fields manually.

{% code %}
{% tab language="json" %}
{
    "img": "base64_image",
    "metadata": {
        "device": "mobile | laptop"
    },
    "secure": {
        "version": "<module version>",
        "token": "<session jwt>",
        "signature": "<payload>"
    }
}
{% /tab %}
{% /code %}

## Response body

This remains the same as the response without the SICAP. Example for /v1/age-antispoofing:

{% code %}
{% tab language="json" %}
{
   "antispoofing": {
       "prediction": "real | fake"
   },
   "age": {
       "st_dev": float,
       "age": float
   }
}
{% /tab %}
{% /code %}

---

## Error codes

SICAP feature introduces new API error codes:

{% synced id="sicap-error-codes" %}
{% /synced %}