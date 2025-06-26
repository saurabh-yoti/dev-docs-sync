---
type: page
title: Quick Start
listed: true
slug: quick-start
description: 
index_title: Quick Start
hidden: 
keywords: 
tags: 
---

We suggest you read through the step by step integration guide to understand the integration in detail. Please see below for a postman collection. 

{% html %}
<div class="alert-BYS">
   <div class="alert-title" id="BYS">
      Before you start
   </div>
   <div class="alert-text" >
      You will need the Yoti App on your phone and to have registered your business with Yoti.
   </div>
   <div class="alert-links"> 
         <a target="_self" href="https://developers.yoti.com/yoti/getting-started">View Onboarding with Yoti</a>
   </div>
</div>
{% /html %}

---

## Postman example

To run the example in postman please click the below button:

{% html %}
<div class="postman-run-button"
data-postman-action="collection/import"
data-postman-var-1="c18a872f5db803fa4d7d"></div>
<script type="text/javascript">
  (function (p,o,s,t,m,a,n) {
    !p[s] && (p[s] = function () { (p[t] || (p[t] = [])).push(arguments); });
    !o.getElementById(s+t) && o.getElementsByTagName("head")[0].appendChild((
      (n = o.createElement("script")),
      (n.id = s+t), (n.async = 1), (n.src = m), n
    ));
  }(window, document, "_pm", "PostmanRunObject", "https://run.pstmn.io/button.js"));
</script>
{% /html %}

---

## Example code

Please see examples for different scenarios. 

### Full example

To use all 6 services:

{% code %}
{% tab language="json" %}
{
    "type": "OVER",
    "age_estimation": {
        "allowed": true,
        "threshold": 25,
        "level": "PASSIVE"
    },
    "digital_id": {
        "allowed": true,
        "threshold": 18,
        "level": "NONE"
    },
    "doc_scan": {
        "allowed": true,
        "threshold": 18,
        "authenticity": "MANUAL",
        "level": "ACTIVE"
    },
    "credit_card": {
        "allowed": false,
        "threshold": 18,
        "level": "NONE"
    },
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

### Over 18 example

{% code %}
{% tab language="json" %}
{
  "type": "OVER",
  "age_estimation": {
    "allowed": true,
    "threshold": 18,
    "level": "MY_FACE"
  },
  "digital_id": {
    "allowed": true,
    "threshold": 18,
    "level": "NONE"
  },
  "doc_scan": {
    "allowed": true,
    "threshold": 18,
    "level": "ACTIVE"
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

### Over 16 example

{% code %}
{% tab language="json" %}
{
  "type": "OVER",
  "age_estimation": {
    "allowed": true,
    "threshold": 16,
    "level": "MY_FACE"
  },
  "digital_id": {
    "allowed": false,
    "threshold": 16,
    "level": "NONE"
  },
  "doc_scan": {
    "allowed": true,
    "threshold": 16,
    "level": "ACTIVE"
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

### Under 40 example

{% code %}
{% tab language="json" %}
{
  "type": "UNDER",
  "age_estimation": {
    "allowed": true,
    "threshold": 40,
    "level": "MY_FACE"
  },
  "digital_id": {
    "allowed": false,
    "threshold": 40,
    "level": "NONE"
  },
  "doc_scan": {
    "allowed": true,
    "threshold": 40,
    "level": "ACTIVE"
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

### Exact age example

{% code %}
{% tab language="json" title="Exact Age" %}
{
  "type": "AGE",
  "age_estimation": {
    "allowed": true,
    "threshold": 13,
    "level": "MY_FACE"
  },
  "digital_id": {
    "allowed": true,
    "threshold": 13,
    "level": "NONE"
  },
  "doc_scan": {
    "allowed": true,
    "threshold": 13,
    "level": "ACTIVE"
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