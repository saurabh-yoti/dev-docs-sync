---
type: page
title: Identity verification
listed: true
slug: identity-verification
description: 
index_title: Identity verification
hidden: 
keywords: 
tags: 
---

Your users will be asked to scan a photo ID document and take a selfie (optional) using the camera on their device. 

The users ID can be analysed to make sure it’s genuine and the document photo is matched to the selfie. 

Good for:

- High assurance
- Global coverage

Yoti will extract the information from the ID document and calculate if you are meet the age requirement using the date of birth. If the image the user has provided is not clear we will ask the user to retry in session. 

You can receive either:

- Age in years
- ‘OVER’ or ‘UNDER’ the age requirement

For extra security, you may also ask the user to take a selfie using the camera on their device. This is to make sure the ID document belongs to the same user and is how we stop fraudsters from impersonating users. Multiple images will be captured and the clearest image will be analysed using face matching technology. This will create a biometric template of the users face, which will be compared to the photo on the ID document.

We store any data captured, such as the ID document and selfie, in our UK data centre. Once the session has been completed, we delete all personal information. If the session is left incomplete then we will delete the data after 25 hours, whichever is sooner. We do not use the data for any other purpose.

{% html %}
<div style="padding:56.25% 0 0 0;position:relative;"><iframe src="https://player.vimeo.com/video/647416549?h=e408543512&amp;badge=0&amp;autopause=0&amp;player_id=0&amp;app_id=58479" frameborder="0" allow="autoplay; fullscreen; picture-in-picture" allowfullscreen style="position:absolute;top:0;left:0;width:100%;height:100%;" title="AVS_IDV_SHORT.mp4"></iframe></div><script src="https://player.vimeo.com/api/player.js"></script>
{% /html %}

If you wish to enable the Identity verification service as an option to perform an age verification service. This solution may take longer to verify your users. 

{% code %}
{% tab language="json" %}
{
    "type": "OVER",
    "doc_scan": {
        "allowed": true,
        "threshold": 18,
        "authenticity": "MANUAL",
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

{% table widths="107,0" %}
| Parameter | Types | Description | 
| ---- | ---- | ---- | 
| allowed | true / false | Enable the verification method to be available for the user to use. | 
| threshold | Integer e.g. 30 | Age threshold for under/over age limits. We recommend this to be the exact age of the threshold you want to cover. | 
| authenticity | OFF / AUTO / MANUAL | If you would like to enable this, Yoti will perform a visual check on the document.  For more information on the types of checks please head [here](/identity-verification/document). | 
| level | NONE / ACTIVE | The level of anti-spoofing for each age verification method.\n\n\nACTIVE enables an active liveness test and face match for IDV. | 
{% /table %}

## Authenticity explained

There are three types of authenticity options that can be performed on the document. 

### Off checks

Once the document is uploaded Yoti will attempt to extract the date of birth. 

### Auto checks

Once the document is uploaded Yoti will attempt to extract the date of birth and perform automated checks on the document:

{% table widths="166" %}
| Sub check | Description | 
| ---- | ---- | 
| document_in_date | If a valid expiration date is present on the document. | 
| fraud_list_check | Yoti will check a fraudulent document database for a match. | 
| ocr_barcode_comparison | This check is performed if fields extracted using OCR from the VIZ (visual inspection zone) of the document and fields extracted from the barcode of a same document both have the mandatory fields populated with values. | 
| doc_number_validation | When there is a driving licence where text extraction has been successful (auto or manual) Yoti will attempt to validate the document number.\n\n\n\nThis check will only be returned for UK Driving licences and Canadian licences (Ontario, Newfoundland and Quebec). | 
{% /table %}

### Manual checks

Once the document is uploaded Yoti will attempt to extract the date of birth and perform automated and manual checks on the document. This includes the checks above and below:

{% table widths="166" %}
| Sub check | Description | 
| ---- | ---- | 
| no_signs_of_forgery | Yoti will assess multiple features of the document to include a wider range of checks.\n\n\n\nYoti will provide a PASS / FAIL breakdown with respective detail on:\n\n\n\n- data_alignment\n- hologram_check\n- security_features_integrity\n- printing_quality\n- fonts_authenticity\n- document_number_integrity | 
| physical_document_captured | This sub check is to verify that the original document was used and not a photocopy. | 
| other_security_features | Yoti will detect if the supplementary security features are valid | 
| no_sign_of_tampering | If Yoti does detect a tampered document we will highlight where. | 
| hologram | Yoti will detect if we can see a shape / colour of the hologram. | 
| hologram_movement | Check hologram movement. | 
{% /table %}

{% badge type="info" text="Hint" /%} This option will take longer to process as the document is being manually reviewed.