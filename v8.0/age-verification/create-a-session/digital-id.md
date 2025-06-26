---
type: page
title: Digital ID
listed: true
slug: digital-id
description: 
index_title: Digital ID
hidden: 
keywords: 
tags: 
---

Here your users scan a QR code using their digital ID app and share a verified age attribute, such as 18+ or 21+.

This requires a one-time onboarding process with an ID document and a selfie. Once created, users are verified for life and can use their digital ID to prove their age or identity details with businesses online and in person.

Good for:

- Reusable authentication
- High assurance
- Global coverage

Yoti will then calculate if the user is acceptable for your age requirement.

You can receive either:

- The age in years
- ‘OVER’ or ‘UNDER’ the age requirement

The user will have a share receipt in their Digital ID app showing what was shared, with whom and when. Yoti also has a share receipt that only contains a date and timestamp, and that a date of birth attribute was provided but we do not store the date of birth itself. We store a encrypted receipt securely in our UK data centre.

{% html %}
<div style="padding:56.25% 0 0 0;position:relative;"><iframe src="https://player.vimeo.com/video/647416655?h=a65d8071f2&amp;badge=0&amp;autopause=0&amp;player_id=0&amp;app_id=58479&dnt=1" frameborder="0" allow="autoplay; fullscreen; picture-in-picture" allowfullscreen style="position:absolute;top:0;left:0;width:100%;height:100%;" title="AVS_YOTI_APP_SHORT.mp4"></iframe></div><script src="https://player.vimeo.com/api/player.js"></script>
{% /html %}

To enable the Digital ID as an option to perform an age verification service.

{% code %}
{% tab language="json" %}
"type": "OVER",
    },
    "digital_id": {
        "allowed": true,
        "threshold": 18
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
| Parameter | Types | Description | 
| ---- | ---- | ---- | 
| allowed | true / false | Enable the verification method to be available for the user to use. | 
| threshold | Integer e.g. 30 | Age threshold for under/over age limits. We recommend this to be the exact age of the threshold you want to cover. | 
{% /table %}