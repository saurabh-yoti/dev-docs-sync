---
type: page
title: Electronic Id
listed: true
slug: electronic-id
description: 
index_title: Electronic Id
hidden: 
keywords: 
tags: 
---

The Electronic ID method allows you to use Swedish Bank ID (Sweden), Mit ID (Denmark) and Finnish Trust Network (Finland) in order to verify a user's age.  If you are looking to perform age checks in any of these countries we recommend offering these methods as an option to users. These eID schemes are widely adopted and regularly used, and therefore should lead to high success rates.

The user will be redirected to the relevant flow where they will be asked to share information from their eID scheme with Yoti in order to verify their age.

{% code %}
{% tab language="json" %}
{
    "type": "OVER",
    "electronic_id": {
      "allowed": true,
      "threshold": 18,
      "sub_methods": [
        "MIT_ID",
        "SWEDISH_BANK_ID",
        "FTN" 
      ]
    }
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

{% table widths="0,163" %}
| Parameter | Types | Description | 
| ---- | ---- | ---- | 
| allowed | true / false | Enable the verification method to be available for the user to use. | 
| sub_methods | MIT_ID / SWEDISH_BANK_ID _/_ FTN | The different electronic ID options available to a user. | 
{% /table %}