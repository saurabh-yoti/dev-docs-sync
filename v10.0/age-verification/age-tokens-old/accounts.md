---
type: page
title: Accounts
listed: true
slug: accounts
description: 
index_title: Accounts
hidden: 1
keywords: 
tags: 
---

To access your site on another device, users can create an age account after their age verification and pass their tokens across to a new browser.

{% image url="https://uploads.developerhub.io/prod/kvAX/35riy6zpm1ldklbjiv12de45gtz2k3qb4660x86t5x0chpyrhxqu7q2bwinjkjs3.png" caption="Age accounts" mode="300" height="676" width="744" %}
{% /image %}

Age accounts are free and anonymous. The age token is stored in an age account, allowing users to access the your site on another browser or device, without having to prove their age again.

This is only available if you use age tokens.  Once the user proves their age via the age methods, they will be given the option to create an account with an anonymous username and password.

{% image url="https://uploads.developerhub.io/prod/kvAX/9dbd7i13zsmgexrywovk1g4autorwarw3tm5iuojfl0yy2urnzgyutudv5cxjtec.png" caption="Age verification complete" mode="600" height="1608" width="1774" %}
{% /image %}

If the user then heads to a website that’s using age accounts, they will click a button to verify your age with Yoti and see an option to log into your age account. 

{% image url="https://uploads.developerhub.io/prod/kvAX/tn7lwoy9wla6712gyuryabjwrulcdmgjcqkorg5dl585ats3cs9icw36hyx6f97m.png" caption="Log in to your account." mode="responsive" height="1696" width="1962" %}
{% /image %}

The user will be prompted to enter your username and password. You will need to check to see if there are any age tokens in your browser that meet the criteria defined by the business linked with your account. If so, Yoti returns a result to confirm if you have previously been verified and your age token meets those criteria.

If the user does not have any age tokens linked to your age account that meet the criteria, the user will be asked to verify their age using one of the available methods. When successful, a new age token will be created and stored in their age account.

{% html %}
<div class="alert-BYS">
   <div class="alert-title" id="BYS">
      Before you start
   </div>
   <div class="alert-text" >
We suggest you have a good read of age tokens and rules   </div>
   <div class="alert-links"> 
   </div>
</div>
{% /html %}

{% code %}
{% tab language="json" %}
"login": {
   "allowed": true
},
"rule_id": "111-111-111-111"
{% /tab %}
{% /code %}

## Full example

{% code %}
{% tab language="json" %}
{
    "type": "OVER",
    "mobile": {
        "allowed": true,
        "threshold": 18,
        "level": "NONE"
    },
    "digital_id": {
        "allowed": true,
        "threshold": 18,
        "level": "NONE"
    },
    "doc_scan": {
        "allowed": true,
        "threshold": 18,
        "level": "NONE"
    },
    "age_estimation": {
        "allowed": true,
        "threshold": 25,
        "level": "NONE"
    },
    "credit_card": {
        "allowed": true,
        "threshold": 18,
        "level": "NONE"
    },
    "ttl": 144000,
    "callback": {
        "auto": false,
        "url": "https://www.yoti.com"
    },
    "login": {
        "allowed": true
    },
    "rule_id": "<uuid>"
}
{% /tab %}
{% /code %}

### Response

{% code %}
{% tab language="json" %}
{
    "sdk_id": "<uuid>",
    "callback_url": "https://your.callback.url",
    "callback": {
        "url": "https://your.callback.url",
        "auto": false
    },
    "notification_url": "https://your.webhook.url",
    "cancel_url": "https://your.cancel.url",
    "type": "OVER",
    "age_estimation": {
        "threshold": 25,
        "allowed": true,
        "level": "NONE"
    },
    "digital_id": {
        "threshold": 18,
        "allowed": true,
        "level": "NONE"
    },
    "doc_scan": {
        "threshold": 18,
        "allowed": true,
        "level": "NONE"
    },
    "credit_card": {
        "threshold": 18,
        "allowed": true,
        "level": "",
        "authenticity": ""
    },
    "mobile": {
        "threshold": 18,
        "allowed": true,
        "level": "",
        "authenticity": ""
    },
    "login": {
        "threshold": 0,
        "allowed": false,
        "level": "",
        "authenticity": ""
    },
    "age": 18,
    "status": "COMPLETE",
    "method": "AGE_ESTIMATION",
    "reference_id": "",
    "created_at": "2021-04-28T14:44:00.263517Z",
    "expires_at": "2030-10-30T20:04:00.263517Z",
    "updated_at": "2021-04-28T14:44:36.056933Z",
    "id": "<uuid>",
    "evidence_id": "<uuid>",
    "rule_id": "<uuid>",
    "biometric_consent_required": true
}
{% /tab %}
{% /code %}