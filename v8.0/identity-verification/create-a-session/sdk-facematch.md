---
type: page
title: Face match
listed: true
slug: sdk-facematch
description: 
index_title: Face match
hidden: 
keywords: 
tags: 
---

If you wish to request a face match check from the user this section will provide you with all the details to complete this. 

Here we describe how to:

- Request a face match check. 

{% table %}
| Name | Resources | Type | Manual check available | 
| ---- | ---- | ---- | ---- | 
| Face match | 1x Doc Resource & 1x Liveness Resource | Asynchronous | ✅ | 
{% /table %}

A request to assess whether the user's face matches the face on the ID document. The user's facial image is obtained from the liveness check, which must be performed first.

{% code %}
{% tab language="javascript" %}
const faceMatchCheck = new RequestedFaceMatchCheckBuilder()
    .withManualCheckFallback()
    .build();
{% /tab %}
{% tab language="java" %}
RequestedFaceMatchCheck faceMatchCheck = RequestedFaceMatchCheck.builder()
    .withManualCheckFallback()
    .build();
{% /tab %}
{% tab language="php" %}
<?php

$faceMatchCheck = (new RequestedFaceMatchCheckBuilder())
    ->withManualCheckFallback()
    ->build();
{% /tab %}
{% tab language="python" %}
faceMatchCheck = RequestedFaceMatchCheckBuilder()
    .with_manual_check_fallback()
    .build()
{% /tab %}
{% tab language="csharp" %}
var faceMatchCheck = new RequestedFaceMatchCheckBuilder()
    .WithManualCheckFallback()
    .Build();
{% /tab %}
{% tab language="go" %}
var faceMatchCheck *check.RequestedFaceMatchCheck
faceMatchCheck, err = check.NewRequestedFaceMatchCheckBuilder().
    WithManualCheckFallback().
    Build()
{% /tab %}
{% tab language="json" %}
{
    "type": "ID_DOCUMENT_FACE_MATCH",
    "config": {
        "manual_check": "FALLBACK"
    }
}
{% /tab %}
{% /code %}

{% table %}
| Manual Check | Explanation | 
| ---- | ---- | 
| withManualCheckFallback | The requested check will only go to the Security Centre if the machine check fails. | 
| withManualCheckNever | The requested check will never go to the Security Centre. | 
| withManualCheckAlways | The requested check will always go to the Security Centre regardless of the success of the automated check.\n\n\n\nNote: This config may result in additional charges. | 
{% /table %}