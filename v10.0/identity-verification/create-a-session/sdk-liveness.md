---
type: page
title: Liveness
listed: true
slug: sdk-liveness
description: 
index_title: Liveness
hidden: 
keywords: 
tags: 
---

If you wish to request a biometric check from the user, this section will provide you with all the details to complete this. Each check will provide a report of the result from the liveness and face match check. 

Here we describe how to:

- Request a liveness check.
- Types of liveness.

{% table widths="" %}
| Name | Resources | Type | Manual check available | 
| ---- | ---- | ---- | ---- | 
| Liveness | 1x Liveness Resource | Synchronous | ❌ | 
{% /table %}

{% html %}
<div class="alert-GTK">
    <div class="alert-title" id="GTK">
        Good to know
    </div>
    <div class="alert-text">
If you require biometric consent for liveness please see how to configure this in session creation preferences.

    </div>
    <div class="alert-links"> 
        <a href="https://developers.yoti.com/identity-verification/system-preferences">Session Preferences</a>
   </div>
</div>
{% /html %}

You must provide the max number of retries your users can have before the liveness is failed. There must be a minimum of 1 attempt. Yoti recommends 3 attempts as a max retry number.

## Request Liveness

Yoti currently provides two types of liveness checks - Static (or Passive) liveness and Zoom (or Active) liveness. We recommended you to use the newer Static liveness that provides a better user experience.

### Static Liveness

{% code %}
{% tab language="javascript" title="Node.js" %}
const livenessCheck = new RequestedLivenessCheckBuilder()
    .forStaticLiveness()
    .withMaxRetries(3)
    .build();
{% /tab %}
{% tab language="java" %}
RequestedLivenessCheck livenessCheck = RequestedLivenessCheck.builder()
    .forStaticLiveness
    .withMaxRetries(3)
    .build();
{% /tab %}
{% tab language="php" %}
<?php

$livenessCheck = (new RequestedLivenessCheckBuilder())
  	->forStaticLiveness()
  	->withMaxRetries(3)
  	->build();
{% /tab %}
{% tab language="python" %}
livenessCheck = RequestedLivenessCheckBuilder()
    .with_liveness_type('STATIC')
    .with_max_retries(3)
    .build()
{% /tab %}
{% tab language="csharp" %}
var livenessCheck = new RequestedLivenessCheckBuilder()
    .ForStaticLiveness()
    .WithMaxRetries(3)
    .Build();
{% /tab %}
{% tab language="go" %}
var livenessCheck *check.RequestedLivenessCheck
livenessCheck, err = check.NewRequestedLivenessCheckBuilder()
    .ForStaticLiveness
    .WithMaxRetries(3)
    .Build()
{% /tab %}
{% tab language="json" %}
{
    "type": "LIVENESS",
    "config": {
        "liveness_type": "STATIC",
        "max_retries": 3
    }
}
{% /tab %}
{% /code %}

### Zoom Liveness

{% code %}
{% tab language="javascript" title="Node.js" %}
const livenessCheck = new RequestedLivenessCheckBuilder()
    .forZoomLiveness()
    .withMaxRetries(3)
    .build();
{% /tab %}
{% tab language="java" %}
RequestedLivenessCheck livenessCheck = RequestedLivenessCheck.builder()
    .forZoomLiveness()
    .withMaxRetries(3)
    .build();
{% /tab %}
{% tab language="php" %}
<?php

$livenessCheck = (new RequestedLivenessCheckBuilder())
  	->forZoomLiveness()
  	->withMaxRetries(3)
  	->build();
{% /tab %}
{% tab language="python" %}
livenessCheck = RequestedLivenessCheckBuilder()
    .for_zoom_liveness()
    .with_max_retries(3)
    .build()
{% /tab %}
{% tab language="csharp" %}
var livenessCheck = new RequestedLivenessCheckBuilder()
    .ForZoomLiveness()
    .WithMaxRetries(3)
    .Build();
{% /tab %}
{% tab language="go" %}
var livenessCheck *check.RequestedLivenessCheck
livenessCheck, err = check.NewRequestedLivenessCheckBuilder()
    .ForZoomLiveness()
    .WithMaxRetries(3)
    .Build()
{% /tab %}
{% tab language="json" %}
{
    "type": "LIVENESS",
    "config": {
        "liveness_type": "ZOOM",
        "max_retries": 3
    }
}
{% /tab %}
{% /code %}

An "attempt" is a completed liveness check that is either rejected or approved. If the user does not complete the liveness check, this does not count as an attempt and the user will be prompted to try again.

The liveness check will create a check response for each attempt, so you should ensure liveness has at least one approval.

{% html %}
<div class="alert-GTK">
    <div class="alert-title" id="GTK">
       Jump to.. 
    </div>
    <div class="alert-text">
       On successful completion, the check outputs a report  which can be found in the ‘retrieve results’ section.
      Details of the report can be found in 'Understanding the report' section.
      
     
    </div>
    <div class="alert-links"> 
        <a href="https://developers.yoti.com/identity-verification/results">Retrieve results</a>
        <a target="_self" href="https://developers.yoti.com/identity-verification/understanding-the-report">Understanding the report</a> 
   </div>
</div>
{% /html %}