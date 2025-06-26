---
type: page
title: Biometric check
listed: true
slug: biometric-checking
description: 
index_title: Biometric check
hidden: 
keywords: 
tags: 
---

If you wish to request a biometric check from the user this section will provide you with all the details to complete this. Each check will provide a report of the result from the liveness and face match check. 

Here we describe how to:

- Request a liveness check.
- Request a face match check. 

{% table %}
| Name | Resources | Type | Manual check available | 
| ---- | ---- | ---- | ---- | 
| Liveness | 1x Liveness Resource | Synchronous | ❌ | 
| Face match | 1x Doc Resource & 1x Liveness Resource | Asynchronous | ✅ | 
{% /table %}

---

## Liveness

A requested check to assess whether the document scan is being performed by a real person, and not someone wearing a mask or an automated system. Whilst the liveness test is being performed Yoti will take 3 images of the user. 

{% badge type="success" text="Hint:" /%} If you require biometric consent for liveness please see how to configure this in session creation preferences.      

You must provide the max number of retries your users can have before the liveness is failed. This must be minimum 1 attempt. Yoti recommends 3 attempts as a max retry number.

{% code %}
{% tab language="javascript" %}
const livenessCheck = new RequestedLivenessCheckBuilder()
    .forZoomLiveness()
    .withMaxRetries(3)
    .build();
{% /tab %}
{% tab language="java" %}
RequestedLivenessCheck livenessCheck = RequestedLivenessCheck.builder().forZoomLiveness().withMaxRetries(3).build();
{% /tab %}
{% tab language="php" %}
<?php

$livenessCheck = (new RequestedLivenessCheckBuilder())
  	->forZoomLiveness()
  	->withMaxRetries(3)
  	->build();
{% /tab %}
{% tab language="python" %}
livenessCheck = RequestedLivenessCheckBuilder().for_zoom_liveness().with_max_retries(3).build()
{% /tab %}
{% tab language="csharp" %}
var livenessCheck = new RequestedLivenessCheckBuilder()
                .ForZoomLiveness()
                .WithMaxRetries(3)
                .Build();
{% /tab %}
{% tab language="go" %}
var livenessCheck *check.RequestedLivenessCheck
livenessCheck, err = check.NewRequestedLivenessCheckBuilder().
	ForZoomLiveness().
	WithMaxRetries(3).
	Build()
{% /tab %}
{% tab language="java" title="Java v2" %}
RequestedLivenessCheck livenessCheck = RequestedCheckBuilderFactory.newInstance().forLivenessCheck()
                .forZoomLiveness().withMaxRetries(3).build();
{% /tab %}
{% /code %}

An "attempt" is a completed liveness check that is either rejected or approved. If the user does not complete the liveness check this does not count as an attempt and the user will be prompted to try again.

{% badge type="success" text="Hint:" /%} The liveness check will create a check response for each attempt, so you should ensure liveness has at least one approval.

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
        <a target="_self" href="https://developers.yoti.com/identity-verification/biometric-report">Understanding the report</a> 
   </div>
</div>
{% /html %}

---

## Face Match

A request to assess whether the user's face matches the face on the ID document. The user's facial image is obtained from the liveness check, which must be performed first.

{% code %}
{% tab language="javascript" %}
const faceMatchCheck = new RequestedFaceMatchCheckBuilder()
    .withManualCheckFallback()
    .build();
{% /tab %}
{% tab language="java" %}
RequestedFaceMatchCheck faceMatchCheck = RequestedFaceMatchCheck.builder().withManualCheckFallback().build();
{% /tab %}
{% tab language="php" %}
<?php

$faceMatchCheck = (new RequestedFaceMatchCheckBuilder())->withManualCheckFallback()->build();
{% /tab %}
{% tab language="python" %}
faceMatchCheck = RequestedFaceMatchCheckBuilder().with_manual_check_fallback().build()
{% /tab %}
{% tab language="csharp" %}
var faceMatchCheck = new RequestedFaceMatchCheckBuilder()
                .WithManualCheckFallback()
                .Build();
{% /tab %}
{% tab language="go" %}
var faceMatchCheck *check.RequestedFaceMatchCheck
faceMatchCheck, err = check.NewRequestedFaceMatchCheckBuilder().
	WithManualCheckAlways().
	Build()
{% /tab %}
{% tab language="java" title="Java v2" %}
RequestedFaceMatchCheck faceMatchCheck = RequestedCheckBuilderFactory.newInstance().forFaceMatchCheck()
        .withManualCheckFallback().build();
{% /tab %}
{% /code %}

{% table %}
| Manual Check | Explanation | 
| ---- | ---- | 
| withManualCheckAlways | The requested check will always go to the Security Centre regardless of the success of the automated check. | 
| withManualCheckNever | The requested check will never go to the Security Centre. | 
| withManualCheckFallback | The requested check will only go to the Security Centre if the machine check fails. | 
{% /table %}