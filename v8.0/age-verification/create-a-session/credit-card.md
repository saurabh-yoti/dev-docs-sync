---
type: page
title: Credit card
listed: true
slug: credit-card
description: 
index_title: Credit card
hidden: 
keywords: 
tags: 
---

Verify your user is over 18 using their credit card details.

This method proves your customer is in possession of a registered credit card, which in most countries, can only be issued to people old enough to sign a credit agreement.

The user will be asked to enter their credit card PAN number, expiry date, postcode and CV2 number.

Yoti will send these details to a payment provider and place a temporary £0.30 hold on the card. This is to verify that the card is current and valid. Yoti will use this to determine that the user is over 18 and remove the £0.30 hold on the card once the age check is complete.

You can receive:

- If you are ‘over’ or ‘under’ their age requirement.

{% image url="https://uploads.developerhub.io/prod/kvAX/6umg8gctb99lw7m5p82ltc9lpthcvp55hy7du3crbzvytq4nc05ywnkowl1d2q4i.png" caption="Credit card check screen" mode="responsive" height="1084" width="566" %}
{% /image %}

We will never store or share the P.A.N. and credit cards will not be charged.

{% html %}
<div style="padding:51.76% 0 0 0;position:relative;"><iframe src="https://player.vimeo.com/video/696594652?h=e26fe5ed30&amp;badge=0&amp;autopause=0&amp;player_id=0&amp;app_id=58479&dnt=1" frameborder="0" allow="autoplay; fullscreen; picture-in-picture" allowfullscreen style="position:absolute;top:0;left:0;width:100%;height:100%;" title="YOTI AV _ CCDebit CARD"></iframe></div><script src="https://player.vimeo.com/api/player.js"></script>
{% /html %}

If you wish to enable the Credit card service as an option to perform an age verification service.

{% code %}
{% tab language="json" %}
{
    "type": "OVER",
    "credit_card": {
        "allowed": true
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

{% table widths="0,136" %}
| Parameter | Types | Description | 
| ---- | ---- | ---- | 
| allowed | true / false | Enable the verification method to be available for the user to use. | 
{% /table %}

## Credit card coverage

Yoti currently supports:

- American Express
- China UnionPay (CUP)
- Discover & Diners
- Japan Credit Bureau (JCB)
- Mastercard
- Visa