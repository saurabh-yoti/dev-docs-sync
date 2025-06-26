---
type: page
title: Mobile
listed: true
slug: mobile
description: 
index_title: Mobile
hidden: 
keywords: 
tags: 
---

Verify your user is over 18 using their mobile provider details.

Mobile phone numbers can be checked against contracts issued by mobile carriers. You should ensure the phone is in the possession of the contract holder before checking their contract and be aware parents will take out contracts for their children.

Good for:

- Accounts linked to a mobile number
- Background checks
- Specific countries

The user enters their name, date of birth, mobile number and their address.

Yoti will send these details to one of our mobile checking providers. The user receives an SMS asking them to confirm the age check by replying to the message. This is to confirm they are in possession of the phone. The provider then confirms that the details entered match the details of the mobile account and Yoti use this to determine that the user is over 18.

You can receive:

- If you are ‘over’ or ‘under’ your age requirement

{% image url="https://uploads.developerhub.io/prod/kvAX/og1nioc9yi4g24anx1z6xep5e5lk6ydx8htn0c0hxoy89tbdt4d63bbn0714dcg6.png" caption="Mobile check" mode="300" height="1028" width="520" %}
{% /image %}

We never store or share the user’s details with anyone other than the provider. 

{% html %}
<div style="padding:51.76% 0 0 0;position:relative;"><iframe src="https://player.vimeo.com/video/696593793?h=54854fc577&amp;badge=0&amp;autopause=0&amp;player_id=0&amp;app_id=58479" frameborder="0" allow="autoplay; fullscreen; picture-in-picture" allowfullscreen style="position:absolute;top:0;left:0;width:100%;height:100%;" title="AVS - Mobile Age Check - SHORT"></iframe></div><script src="https://player.vimeo.com/api/player.js"></script>
{% /html %}

If you wish to enable the mobile service as an option to perform an age verification service.

{% code %}
{% tab language="json" %}
{
    "type": "OVER",
    "mobile": {
        "allowed": false,
        "threshold": 18,
        "level": "NONE"
    },
    "ttl": 900,
    "reference_id": "over_18_example",
    "callback": {
       "auto": true,
       "url": "https://www.yoti.com"
    },
    "notification_url": "https://yourdomain.example/webhook",
    "block_biometric_consent": false,
    "cancel_url": "https://www.yoti.com"
}
{% /tab %}
{% /code %}

{% table widths="0,137" %}
| Parameter | Types | Description | 
| ---- | ---- | ---- | 
| allowed | true / false | Enable the verification method to be available for the user to use. | 
| threshold | Integer e.g. 18 | Age threshold for under/over age limits. We recommend this to be the exact age of the threshold you want to cover. | 
| level | NONE | The level of anti-spoofing for each age verification method. | 
{% /table %}

{% badge type="info" text="Hint" /%}Although this option is low friction for the user, there is a risk due to shared phones amongst parents and children.