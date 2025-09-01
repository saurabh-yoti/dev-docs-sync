---
type: page
title: Report
listed: true
slug: liveness-report
description: 
index_title: Report
hidden: 
keywords: 
tags: 
---

Yoti will provide a recommendation for the liveness check.

{% html %}
<div class="alert-GTK">
    <div class="alert-title" id="GTK">
        Good to know
    </div>
    <div class="alert-text">
       Yoti will provide back all images and results from all liveness attempts. 
    </div>
    <div class="alert-links"> 
   </div>
</div>
{% /html %}

{% table widths="152" %}
| Response | Description | 
| ---- | ---- | 
| 🟢  APPROVE | The user has passed the liveness test. | 
| 🔴 REJECT | The liveness check has failed; the user may retry until all attempts are exhausted. | 
| **🟠** NOT AVAILABLE | The liveness check has been unable to be completed | 
{% /table %}

## Liveness types

As part of the liveness check, Yoti performs the following sub check on the face capture explained below which will either PASS or FAIL.

#### Active (Zoom) Liveness

{% table %}
| Sub check | Description | 
| ---- | ---- | 
| liveness_auth | Whether the liveness could be authenticated as a real person or not.\n\nIf value is FAIL, the check will recommend REJECT with no reason given. | 
{% /table %}

#### Passive (Static) Liveness

{% table %}
| Sub check | Description | 
| ---- | ---- | 
| liveness_auth | Whether the liveness could be authenticated as a real person or not. If value is FAIL, the check will recommend REJECT with no reason given. | 
| face_processing | Face detected and processed by the Liveness model. If value is FAIL, the check will recommend REJECT. | 
| payload_signature_verification | Integrity check to ensure images captured are not modified and have been taken live by the user. If value is FAIL, the check will recommend REJECT. | 
{% /table %}

---

## Request a liveness check

If you would like to request this check you can in two ways:

- Use our portal.
- Use our SDK.