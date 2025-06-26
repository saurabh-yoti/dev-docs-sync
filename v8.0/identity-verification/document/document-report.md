---
type: page
title: Report
listed: true
slug: document-report
description: 
index_title: Report
hidden: 
keywords: 
tags: 
---

Yoti performs numerous checks on a document in order to generate this report. Yoti will also provide a recommendation for the authenticity of the document:

{% table widths="212" %}
| Recommendation | Explained | 
| ---- | ---- | 
| 🟢 APPROVE | The document has passed Yoti verification standards. | 
| 🔴  REJECT | The document could be tampered or a counterfeit. Yoti recommends you flag users that are rejected. | 
| **🟠** NOT_AVAILABLE | Yoti couldn’t perform the check, usually due to the quality of submitted images or user error. | 
{% /table %}

As part of the document check, Yoti performs multiple sub checks on the document explained below. The results for the sub checks will be PASS or FAIL. All sub checks state whether the check was performed through a manual process (Expert Review), or through Automation.

{% html %}
<div class="alert-GTK">
    <div class="alert-title" id="GTK">
       Good to know
    </div>
    <div class="alert-text">
       The report breakdown will only display sub-checks that have been attempted.
    </div>
    <div class="alert-text">
       Sub-checks designated as 'Automated' require document data to be extracted, and therefore the data extraction task to be configured.
    </div>
    <div class="alert-links"> 
   </div>
</div>
{% /html %}

{% table widths="166,527" %}
| Sub check | Description | Automated | 
| ---- | ---- | ---- | 
| no_signs_of_forgery | Yoti will assess multiple features of the document to include a wider range of checks.\n\n\n\nOn failure, Yoti will provide a PASS / FAIL breakdown with respective detail on:\n\n\n\n- data_alignment\n- hologram_check\n- security_features_integrity\n- printing_quality\n- fonts_authenticity\n- document_number_integrity | ❌ | 
| no_sign_of_tampering | If Yoti does detect a tampered document we will highlight where. | ❌ | 
| hologram | Yoti will detect if we can see a shape / colour of the hologram. | ❌ | 
| hologram_movement | Check hologram movement. | ❌ | 
| other_security_features | Yoti will detect if the supplementary security features are valid | ❌ | 
| physical_document_captured | This sub check is to verify that the original document was used and not a photocopy. | ❌ | 
| document_in_date | If a valid expiration date is present on the document. | ✅ | 
| fraud_list_check | Yoti will check a fraudulent document database for a match. | ✅ | 
| ocr_barcode_comparison | This check is performed if fields extracted using OCR from the VIZ (visual inspection zone) of the document and fields extracted from the barcode of a same document both have the mandatory fields populated with values. | ✅ | 
| doc_number_validation | When there is a driving licence where text extraction has been successful (auto or manual) Yoti will attempt to validate the document number.\n\n\n\nThis check will only be returned for UK Driving licences and Canadian licences (Ontario, Newfoundland and Quebec). | ✅ | 
| mrz_validation | Validates that the MRZ of the document is in the expected format. | ✅ | 
| ocr_mrz_comparison | Comparison between the visual inspection zone of the document and the MRZ. This check would commonly be performed for Passports, but can be run on other documents that have an MRZ. | ✅ | 
| issuing_authority | This sub-check checks the document information against the Issuing Authorities records. Only triggers if the requested check is enabled, with a document that supports the check. | ✅ | 
| age_estimation_dob_comparison | This sub-check performs an Age estimation on the captured selfie, comparing it to the ID document date of birth.\n\n\nFor more details on Yoti's Age Estimation, read our White Paper [here](https://www.yoti.com/blog/yoti-age-white-paper/). | ✅ | 
| chip_parse | If chip data is present | ✅ | 
| chip_sod_parse | If Security Object document is present | ✅ | 
| chip_data_integrity | Checks the data integrity on the chip | ✅ | 
| chip_digital_\n\nsignature_verification | Verifies the digital signature and trust chain | ✅ | 
| chip_csca_trusted | Checks if the Country Signing Certification Authority (CSCA) Certificate is trusted | ✅ | 
| yoti_fraud_list_check | Checks against Yoti's fraud watchlist for a match on the ID document. This sub-check will always be performed, is returned as PASS when no match is found, or FAIL when there is a match. For cases where a possible match is found, the session will be sent for additional manual checks to determine the final check outcome. | ✅ | 
{% /table %}

---

## Rejection report

For the list of rejection suggestions please see below which will allow you to provide the user a correction attempt:

{% table %}
| Yoti Reason | Recovery suggestions | 
| ---- | ---- | 
| COUNTERFEIT | You may want to flag this user. | 
| EXPIRED_DOCUMENT | Ask the user to try again with a different document. | 
| FRAUD_LIST_MATCH | You may want to flag this user. | 
| DOCUMENT_COPY | Ask the user to try again with the original document. | 
| ISSUING_AUTHORITY_INVALID | You may want to flag this user. | 
| TAMPERED | You may want to flag this user. | 
| MISSING_HOLOGRAM | Ask the user to try again with capture method / in a brighter area. | 
| NO_HOLOGRAM_MOVEMENT | Ask the user to try again with capture method  / in a brighter area. | 
| DATA_MISMATCH | You may want to flag this user. | 
| DOC_NUMBER_INVALID | You may want to flag this user. | 
| CHIP_DATA_INTEGRITY_FAILED | You may want to flag this user. | 
| CHIP_SIGNATURE_VERIFICATION_FAILED | You may want to flag this user. | 
| CHIP_CSCA_VERIFICATION_FAILED | You may want to flag this user. | 
{% /table %}

## Not available report

If Yoti was unable to perform checks here is a list of the responses we will return:

{% table %}
| Yoti Reason | Recovery suggestions | 
| ---- | ---- | 
| PHOTO_OVEREXPOSED | Ask the user to try again ensuring no excessive light is on the document. | 
| PHOTO_TOO_DARK | Ask the user to try again and move into a lighter area. | 
| PHOTO_TOO_BLURRY | Ask the user to try again with the ID document on a flat surface, or to use their mobile. | 
| DOCUMENT_TOO_DAMAGED | Ask the user to try again with a different ID document. | 
| GLARE_OBSTRUCTION | Ask the user to try again. | 
| OBJECT_OBSTRUCTION | Ask the user to try again and ensure you can see the ID fully. | 
| NO_DOCUMENT | Ask the user to try again and to upload a document. | 
| PARTIAL_PHOTO | Ask the user to try again and ensure you can see the ID fully. | 
| IMAGE_RESOLUTION_TOO_LOW | Ask the user to try again and to use their mobile. | 
| COUNTRY_NOT_SUPPORTED | The user may not be able to complete the process with Yoti. | 
| DOCUMENT_NOT_SUPPORTED | Ask the user to try again with a different document. | 
| INCORRECT_DOCUMENT_TYPE | Ask the user to try again with the correct selected document. | 
| INCORRECT_MRZ | Ask the user to try again with a different document. | 
| DOCUMENT_VERSION_NOT_SUPPORTED | Ask the user to try again with a different document. | 
| MISSING_DOCUMENT_SIDE | Ask the user to try again sending through both sides of the document. | 
| BLACK_AND_WHITE_IMAGE | Ask the user to try again with a different document or coloured document. | 
| MISUSE | Ask the user to try again with a different document. | 
| INVALID | Ask the user to try again with a different document. | 
| CHIP_PARSE | Ask the user to try again with a different document. | 
| CHIP_SOD_PARSE | Ask the user to try again with a different document. | 
{% /table %}

---

## Document comparison check

Yoti performs the following sub check explained below which will either be a PASS or a FAIL.

Document comparison compares values of 2 different documents. This is always done automatically.

{% table %}
| Sub check | Description | Automated | 
| ---- | ---- | ---- | 
| dob_match | If both documents have date of birth, they will be compared. | ✅ | 
| name_match | If both documents have name, they will be compared. | ✅ | 
{% /table %}

For the list of rejection suggestions please see below which will allow you to provide the user a correction attempt:

{% table %}
| Yoti response | Recovery suggestion | 
| ---- | ---- | 
| MISMATCH | Ask the user to try again and check their documents have the same attributes. | 
{% /table %}

If Yoti was unable to perform checks here is a list of the responses we will return:

{% table %}
| Yoti Response | Recovery suggestion | 
| ---- | ---- | 
| NON_LATIN_CHARACTER_IN_NAME | Ask the user to try again with latin characters on their document. | 
| NO_VALID_SUBCHECKS | Ask the user to try again making sure the data is present on the documents. | 
{% /table %}

{% html %}
<div class="alert-GTK">

    <div class="alert-title" id="GTK">

        Good to know

    </div>

    <div class="alert-text">

For Supported documents we will complete a NAME comparison. For two ID documents we will do a DOB and a NAME comparison.
    </div>


    </div>

</div>
{% /html %}

---

## Request document check

If you would like to request this check you can in two ways: 

- Use our [portal](https://developers.yoti.com/identity-verification/portal-guide#request-id-document-check).
- Use our [SDK](https://developers.yoti.com/identity-verification/document-checking) or [API](https://yoti.world/yoti-public-api/#/Backend%20Endpoints/post_sessions).