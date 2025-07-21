---
type: page
title: Configurable Flow
listed: false
slug: shortened-user-flow
description: 
index_title: Configurable Flow
hidden: 
keywords: 
tags: 
---

Integrators have the ability to Shorten the Yoti user interface by skipping certain screens. This can improve the user experience by not duplicating information that integrators may have already shared with users.

The ability to skip screens can be configured in the "sdk config" by including the specific screens that you want to be skipped as outlined below:

{% code %}
{% tab language="java" %}
SdkConfig sdkConfig = SdkConfig.builder()
    .withPrimaryColour("#2d9fff")
  	.withLocale("en-GB")
    .withPresetIssuingCountry("GBR")
    .withSuccessUrl("https://localhost:8443/success")
    .withErrorUrl("https://localhost:8443/error")
    .withAllowHandoff(true)
    .withSuppressedScreen("ID_DOCUMENT_EDUCATION")
    .withSuppressedScreen("FACE_CAPTURE_EDUCATION")
    .withSuppressedScreen("STATIC_LIVENESS_EDUCATION")
    .build();
{% /tab %}
{% tab language="json" %}
{
  "sdk_config": {
    "allowed_capture_methods": "CAMERA_AND_UPLOAD",
     ...
    "attempts_configuration": {
      "ID_DOCUMENT_TEXT_DATA_EXTRACTION": {
        "GENERIC": 3,
        "RECLASSIFICATION": 2
      }
    },
    "suppressed_screens": [
      "ID_DOCUMENT_EDUCATION",
      "ID_DOCUMENT_REQUIREMENTS",
      "ZOOM_LIVENESS_EDUCATION",
      "STATIC_LIVENESS_EDUCATION",
      "FACE_CAPTURE_EDUCATION",
      "FLOW_COMPLETION"
    ]
  }
  ...
}
{% /tab %}
{% /code %}

Skippable Screens:

{% table widths="" %}
| Screen | Description | 
| ---- | ---- | 
| ID_DOCUMENT_EDUCATION | Screen that gives users information about how to capture a good image of their ID document | 
| ID_DOCUMENT_REQUIREMENTS | Screen that allows users to select which ID document to use. This screen should only be skipped if you are enforcing the use of a specific document | 
| FACE_CAPTURE_EDUCATION | Screen that gives users information about how to capture a good face capture image. | 
| STATIC_LIVENESS_EDUCATION | Screen that gives users information about the static liveness check. | 
| ZOOM_LIVENESS_EDUCATION | Screen that gives users information about the zoom liveness check. | 
| FLOW_COMPLETION | Completion screen that uses sees at the end of the flow. Can only be skipped in our native sdk's. Not applicable for the web sdk. | 
{% /table %}

The flow will look as follows with all screens skipped:

{% image url="https://uploads.developerhub.io/prod/kvAX/ztrlb3lpn1u2z0wexcjvhnm4qrctryz2sl1r6m50aakockpzlxjjbpeoo5qsufqn.png" mode="set" height="812" width="470" %}
{% /image %}

{% image url="https://uploads.developerhub.io/prod/kvAX/det6usradmn1u80dx7iu4hselrdvtby57od6japr1dtel3yt0i4uqbjjxsxr6nxj.png" mode="set" height="816" width="472" %}
{% /image %}

{% image url="https://uploads.developerhub.io/prod/kvAX/vt8wmwwtq7jyzjzu8isr9ei7v5648o4roolmzg01ohq2v3v4i2dnacrvsqbqen7y.png" mode="set" height="450.140625" width="227" %}
{% /image %}

{% callout type="warning" title="Important" %}
Please contact us in order to use this feature. we will need to review your current UX.
{% /callout %}