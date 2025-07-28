---
type: page
title: Reusable checks
listed: true
slug: age-tokens2
description: 
index_title: Age Tokens2
hidden: 
keywords: 
tags: 
---

When a user visits a restricted content website, they’re sent to the portal to verify their age. Yoti identifies the content provider, the age requirement, and any criteria specified for the verification. With this information, Yoti create a credential subject that contains the age token and a credential proof that contains a digital signature that proves the credential was issued by Yoti. 

{% image url="https://uploads.developerhub.io/prod/kvAX/9ikfpbyacdv1zlie3hzwmaeicttpdnhxo234omtkj4t3dmcsh892j5iayma3ak3z.png" caption="Age token" mode="responsive" height="506" width="1944" %}
{% /image %}

Tokens are flexible and are accepted entirely at the discretion of the integrating party. You can define your own criteria for what type of age tokens you accept, depending on your regulatory requirements.

When the user lands on your site there will be a token request, a check is performed to see if the user has an age claim that matches your requirements.

If a user doesn’t have a token that meets the requirements, they’ll be sent to your age portal to prove their age again.

If a user doesn’t have a token that meets your requirements, they’ll be sent through the age verification process to prove their age again. You will need to add rules to your configuration e.g. 

- The maximum **time** that a token can be considered valid.
- The **method** of age verification used.
- The **type of age** recorded (an “Over/Under Age” or date of birth)
- The **age threshold** a user must fall within.
- The **type of liveness check** performed.
- The **type of authenticity check** performed.

To test out the flow of an age token please [try this demo](https://yoti.world/glamour-demo/). You will need the first tile: Visitor access.

There are two steps that need to take place in order to use age tokens:

- Create age token rule
- Configure yoti_keys method

---

{% synced id="create-age-rule" %}
{% /synced %}

---

## Configure yoti_key Method

Now that a rule id has been generated, it can be used in the session creation configuration to understand what conditions the age token needs to satisfy. You will also need to configure the "yoti_key" method, to enable the age token functionality.

{% code %}
{% tab language="json" %}
{
    "type": "OVER",
    "age_estimation": {
        "allowed": true,
        "threshold": 25,
        "level": "PASSIVE",
        "retry_limit": 1
    },
    "digital_id": {
        "allowed": true,
        "threshold": 18,
        "level": "NONE",
        "retry_limit": 1
    },
    "doc_scan": {
        "allowed": true,
        "threshold": 18,
        "authenticity": "AUTO",
        "level": "PASSIVE",
        "retry_limit": 1
    },
    "yoti_key": {
      "allowed": true,
      "authentication": false
    },
    "rule_id": "your_rule_id",
    "ttl": 900,
    "reference_id": "over_18_example",
    "callback": {
       "auto": true,
       "url": "https://www.yoti.com"
    },
    "notification_url": "https://yourdomain.example/webhook",
    "cancel_url": "https://www.yoti.com",
    "retry_enabled": false,
    "resume_enabled": false,
    "synchronous_checks": true
}
{% /tab %}
{% /code %}

{% table widths="" %}
| Field | Types | Description | 
| ---- | ---- | ---- | 
| allowed | true / false | Enable the verification method to be available for the user to use. | 
| authentication | true / false | False:  When the Yoti user interface is launched we immediately check if the user has a token that matches the requirements set in the rule. If it matches, the user is immediately directed to the callback url.\n\n\n\nTrue: When users finish any of the Yoti age verification methods, they have the option to create a Yoti age key. They can then use this age key to quickly pass any future age verification sessions that they need to undergo. If authentication is set to true, The Yoti user interface will be shown, the user can then select the yoti_key method to verify their age, or they can use another method in the UI. | 
{% /table %}