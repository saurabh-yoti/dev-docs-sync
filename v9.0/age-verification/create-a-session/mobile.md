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

{% synced id="mobile-avs-overview" %}
{% /synced %}

{% image url="https://uploads.developerhub.io/prod/kvAX/jszzckid95m590ac9xzesfurxq0dbutqy71gj0q7dpjxxu0c0rf2y9aqrxmykq1y.png" mode="responsive" height="1028" width="520" %}
{% /image %}

{% html %}
<div style="padding:51.76% 0 0 0;position:relative;"><iframe src="https://player.vimeo.com/video/696593793?h=54854fc577&amp;badge=0&amp;autopause=0&amp;player_id=0&amp;app_id=58479&dnt=1" frameborder="0" allow="autoplay; fullscreen; picture-in-picture" allowfullscreen style="position:absolute;top:0;left:0;width:100%;height:100%;" title="AVS - Mobile Age Check - SHORT"></iframe></div><script src="https://player.vimeo.com/api/player.js"></script>
{% /html %}

If you wish to enable the mobile service as an option to perform an age verification service.

{% code %}
{% tab language="json" %}
{
    "type": "OVER",
    "mobile": {
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

{% table widths="0,137" %}
| Parameter | Types | Description | 
| ---- | ---- | ---- | 
| allowed | true / false | Enable the verification method to be available for the user to use. | 
{% /table %}

{% badge type="info" text="Hint" /%}Although this option is low friction for the user, there is a risk due to shared phones amongst parents and children.