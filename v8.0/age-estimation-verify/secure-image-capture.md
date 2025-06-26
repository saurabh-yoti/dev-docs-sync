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

Yoti age estimation also supports SICAP (Secure Image Capture) which works alongside the web browser face capture module. This ensures the captured image has not been manipulated (for e.g., injection attacks) before it is submitted to the Yoti backend for processing.

In order to use SICAP, you will need to:

- Use Yoti’s React/JS [Face Capture Module (FCM)](https://www.npmjs.com/package/@getyoti/react-face-capture) version 1.0.0 or later.
- Use the fields **"img"** and **"secure"** from FCM output.
- Add a query parameter when calling the Yoti API endpoints.
- Modify the API request body with a **"secure"** output added.

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

## Endpoints

If you wish to use the secure feature, you will need to add the query parameter ‘?secure=true’ to the applicable endpoint below:

- /v1/age-verify?secure=true
- /v1/age-antispoofing-verify?secure=true

{% badge type="warning" text="Note:" /%} if secure is requested, you will also need to add a **“secure”** field in the request body, or you will get an **'INVALID_REQUEST_BODY'** error message.

### Request body

{% code %}
{% tab language="json" %}
{
    "img": "base64_image",
    "threshold": "age_threshold",
    "operator": "OVER" | "UNDER",
    "metadata": (Optional) {        
        "device": "mobile", "laptop", "unknown"
    },
    "secure": (optional) {
        "version": <module version>
        "token": <session jwt>
        "signature": <payload>
        "verification": <verification-data>
    }
}
{% /tab %}
{% /code %}

Use the “img” and “secure” fields that are automatically returned from the Face capture module on success. Do not modify these fields manually.

### Response body

{% code %}
{% tab language="json" %}
{
    "antispoofing": {
			"prediction": "real | fake" 
		}
	"age": {
			"age_check": "pass | fail" (string)     
		}
}
{% /tab %}
{% /code %}

This remains the same as the response without the SICAP.

## Error codes

SICAP feature introduces new API error codes:

{% synced id="sicap-error-codes" %}
{% /synced %}