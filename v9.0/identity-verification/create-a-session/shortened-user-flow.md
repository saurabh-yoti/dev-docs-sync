---
type: page
title: Shortened Flow
listed: true
slug: shortened-user-flow
description: 
index_title: Shortened Flow
hidden: 
keywords: 
tags: 
---

Integrators have the ability to Shorten the Yoti user interface by skipping certain screens. This can improve the user experience by not duplicating information that integrators may have already shared with users.

The ability to skip screens can be configured in the "sdk_config" by including specific screens in the "suppressed_screens" array as outlined below:

{% code %}
{% tab language="java" %}
SdkConfig sdkConfig = SdkConfig.builder()
    .withPrimaryColour("#2d9fff")
  	.withLocale("en-GB")
    .withPresetIssuingCountry("GBR")
    .withSuccessUrl("https://localhost:8443/success")
    .withErrorUrl("https://localhost:8443/error")
    .withAllowHandoff(true)
    .withSuppressedScreens(Arrays.asList("FACE_CAPTURE_EDUCATION", "STATIC_LIVENESS_EDUCATION"))
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
      "ZOOM_LIVENESS_EDUCATION",
      "STATIC_LIVENESS_EDUCATION",
      "FACE_CAPTURE_EDUCATION",
      "FLOW_COMPLETION",
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
| FACE_CAPTURE___EDUCATION | Screen that gives users information about how to capture a good image. | 
| STATIC_LIVENESS_EDUCATION | Screen that gives users information about the static liveness check. | 
| ZOOM_LIVENESS_EDUCATION | Screen that gives users information about the zoom liveness check. | 
| FLOW_COMPLETION | Completion screen that uses sees at the end of the flow. | 
{% /table %}

The normal flow looks as follows:

{% image url="https://uploads.developerhub.io/prod/kvAX/lufl9he6qew03bep0bbq0auag9pbxv9cb4431g3uf072t30jwqt0isvj2xte2ju6.png" mode="responsive" height="700" width="354" %}
{% /image %}

{% image url="https://uploads.developerhub.io/prod/kvAX/w85wy3ke4rkr3dch2nsjb1aj9a4zkpccw2i5z0lwld6bsfgu9ua9b2polp9ai98c.jpeg" mode="responsive" height="700" width="407" %}
{% /image %}

{% image url="https://uploads.developerhub.io/prod/kvAX/v0g2pejj6gysrc5mh7vtmjva0wmnj5w2md7chz6diis1t3hiuuytta1gw37n4xwn.png" mode="responsive" height="700" width="353" %}
{% /image %}

{% image url="https://uploads.developerhub.io/prod/kvAX/hbpfox3r13rgjcyqfv8m0ig38sfntvbqorechxhkgn2tmfve9yg2hdgaim0izt67.png" mode="responsive" height="700" width="353" %}
{% /image %}

{% image url="https://uploads.developerhub.io/prod/kvAX/t5ntinq57jwgatc2ogt2xeuuvgexu69vc2sw06hqg1z3hovam9tddbkc3blazi56.jpeg" mode="responsive" height="700" width="412" %}
{% /image %}

But If the Face Capture Education, the Liveness Education and the Flow Completion screens are skipped the flow will look as follows:

{% image url="https://uploads.developerhub.io/prod/kvAX/xw5mw2i7g7jsautrk835hrml4swgkw0dztro8msv94fb7ceagbzrq6nk519osl5f.png" caption="Liveness Screen 1" mode="responsive" height="700" width="354" %}
{% /image %}

{% image url="https://uploads.developerhub.io/prod/kvAX/v5fe72abm5g060s7ew3gm22q4dsql4fqce923m2qbbpqluedueaeapo55leqhnm7.png" caption="Liveness Screen 2" mode="responsive" height="700" width="353" %}
{% /image %}

{% image url="https://uploads.developerhub.io/prod/kvAX/u6z45gnktu47vp1jny5mnsdpuhgp72487cquv87ug9ovdgpmt26wamhzk3nquxqu.png" caption="Liveness Screen 3" mode="responsive" height="700" width="353" %}
{% /image %}

The user will be immediately redirected to your callback url after the above screen.

{% callout type="warning" title="Important" %}
Please contact us in order to use this feature. we will need to review your current UX.
{% /callout %}