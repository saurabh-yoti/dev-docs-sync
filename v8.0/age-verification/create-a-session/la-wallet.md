---
type: page
title: LA Wallet
listed: true
slug: la-wallet
description: 
index_title: LA Wallet
hidden: 
keywords: 
tags: 
---

Yoti offers the additional method of using a LA wallet to verify a users age.

The La wallet method is similar to our own digital id method, but instead of a QR code that needs to be scanned, we will present a numerical code on the screen which the user will need to enter into their LA wallet app. By going to the "Verify You" tab and tapping on the "Remote Verify" button at the top of the screen, the user will enter the code that we present to accept or deny the verification request.

{% code %}
{% tab language="json" %}
{
    "type": "OVER",
    "la_wallet": {
      "allowed" : true,
      "threshold": 21
    },
    "ttl": 900,
    "reference_id": "over_18_example",
    "callback": {
       "auto": true,
       "url": "https://www.yoti.com"
    },
    "notification_url": "https://yourdomain.example/webhook",
    "cancel_url": "https://www.yoti.com"
}
{% /tab %}
{% /code %}

{% table %}
| Parameters | Types | Description | 
| ---- | ---- | ---- | 
| allowed | true / false | Enable the verification method to be available for the user to use. | 
| threshold | Integer e.g. 30 | Age threshold for under/over age limits. We recommend this to be the exact age of the threshold you want to cover. | 
{% /table %}