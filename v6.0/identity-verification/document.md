---
type: page
title: Document
listed: true
slug: document
description: 
index_title: Document
hidden: 
keywords: 
tags: 
---

If you wish to request a document from the user this section will provide you context on what this check entails. Each check will provide a report of the result from the document check. 

The user will have the option to upload an image or take a photo, this is configurable in your session creation. Yoti recommends you have both options available. 

This section will describe:

- What document checks are available.
- What documents Yoti supports.
- What checks does Yoti perform.
- Rejection results
- Not available results

---

## Document checks

The below checks are related to document checks available at Yoti:

{% table widths="0,0,242,0" %}
| Name | Description | Resources | Type | Manual check available | 
| ---- | ---- | ---- | ---- | ---- | 
| Document authenticity | A request to assess the characteristics of a document, to determine the validity of the ID document. Yoti will perform multiple checks on a ID document. | 1x Document Resource | Asynchronous | ✅ | 
| Text extraction | A request to obtain the data printed visually on a document, in structured form. | 1x Document Resource | Asynchronous | ✅ | 
| Supporting documents | Yoti offers the ability to request additional documents to enhance the verification of the user. | 1x Document Resource | Asynchronous | ✅ | 
| Document comparison | If you request your users to upload more than one document we offer the ability to cross check the data | 2x Document Resource | Asynchronous | ❌ | 
| Filters | Restriction of documents / countries. If you do not wish to accept all documents or countries you can configure your session to add / remove which countries and document types are displayed to the user on the user view. | N/A | N/A | N/A | 
| Supported documents | List of documents supported | N/A | N/A | N/A | 
{% /table %}

Features to enhance the document check:

- Document preferences - removing available documents / countries.
- Near Field Communication (NFC)
- Address check
- AML check

---

## Document list

Yoti supports the following types of documents:

{% table widths="385" %}
| Type | Country | 
| ---- | ---- | 
| Passport | Global | 
| Driving license | Global | 
| National ID | Global | 
| PAN, Aadhaar | India | 
| Mykad | Malaysia | 
| Biometric residence permit | United Kingdom, Canada, Belgium, Cyprus, Italy,Netherlands, Norway, Spain, Sweden, Denmark, Estonia, France, Latvia, Malta, Poland, Portugal, Slovakia, Switzerland, Hungary, Luxembourg, Taiwan, Afghanistan | 
| Health Card | Canada | 
| Residence permit, Nexus card | Canada | 
| Postal ID, Professional ID, SSS ID, Voter ID, UMID | Philippines | 
| State ID | United states | 
| Bank statement | Global | 
| Council Tax bill | Global | 
| Phone bill | Global | 
| Utility bill | Global | 
{% /table %}

Yoti now supports some non-latin character documents:

{% badge type="info" text="Hint" /%} Yoti will attempt to do automated text extraction only on these documents and a document authenticity check. We cannot perform manual text extractions on these documents.

{% table %}
| Type | Country | 
| ---- | ---- | 
| Driving license | China, Japan, Russia | 
| National ID | China, Japan, Egypt, Kazakhstan, Russia | 
{% /table %}

{% html %}
<div class="alert-GTK">

    <div class="alert-title" id="GTK">

        Good to know

    </div>

    <div class="alert-text">

If Yoti is missing a document you would like us to support please feel free to get in touch with us and we will investigate the documents security features and templates. Use our SDK to get a full list of the supported documents. 
    </div>


    </div>

</div>
{% /html %}

To see a full list of supported documents use our [supported documents endpoint.](/identity-verification/document-checking#supported-documents)

---

## The results

Yoti performs numerous checks on a document in order to generate this report. Yoti will also provide a recommendation for the authenticity of the document:

{% table widths="162" %}
| Recommendation | Explained | 
| ---- | ---- | 
| APPROVE 🟢 | The document has passed Yoti verification standards. | 
| REJECT 🔴 | The document could be tampered or a counterfeit. Yoti recommends you flag users that are rejected. | 
| NOT_AVAILABLE **🟠** | Yoti couldn’t perform the check, usually due to the quality of submitted images or user error. | 
{% /table %}

As part of the document check, Yoti performs multiple sub checks on the document explained below. The results for the sub checks will be PASS or FAIL.

{% badge type="success" text="Hint: " /%} Only checks attempted will be shown in the response.

{% table widths="166,527" %}
| Sub check | Description | Automated | 
| ---- | ---- | ---- | 
| no_signs_of_forgery | Yoti will assess multiple features of the document to include a wider range of checks.\n\n\n\nYoti will provide a PASS / FAIL breakdown with respective detail on:\n\n\n\n- data_alignment\n- hologram_check\n- security_features_integrity\n- printing_quality\n- fonts_authenticity\n- document_number_integrity | ❌ | 
| document_in_date | If a valid expiration date is present on the document. | ✅ | 
| fraud_list_check | Yoti will check a fraudulent document database for a match. | ✅ | 
| physical_document_captured | This sub check is to verify that the original document was used and not a photocopy. | ❌ | 
| other_security_features | Yoti will detect if the supplementary security features are valid | ❌ | 
| no_sign_of_tampering | If Yoti does detect a tampered document we will highlight where. | ❌ | 
| hologram | Yoti will detect if we can see a shape / colour of the hologram. | ❌ | 
| hologram_movement | Check hologram movement. | ❌ | 
| ocr_barcode_comparison | This check is performed if fields extracted using OCR from the VIZ (visual inspection zone) of the document and fields extracted from the barcode of a same document both have the mandatory fields populated with values. | ✅ | 
| doc_number_validation | When there is a driving licence where text extraction has been successful (auto or manual) Yoti will attempt to validate the document number.\n\n\n\nThis check will only be returned for UK Driving licences and Canadian licences (Ontario, Newfoundland and Quebec). | ✅ | 
| issuing_authority - COMING SOON | This sub-check checks the document information against the Issuing Authorities records. Currently this only happens for AAMVA. | ✅ | 
| chip_parse | If chip data is present | ✅ | 
| chip_sod_parse | If Security Object document is present | ✅ | 
| chip_data_integrity | Checks the data integrity on the chip | ✅ | 
| chip_digital_\n\nsignature_verification | Verifies the digital signature and trust chain | ✅ | 
| chip_csca_trusted | Checks if the Country Signing Certification Authority (CSCA) Certificate is trusted | ✅ | 
{% /table %}

### Rejection result

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
| CHIP_DATA_INTEGRITY_FAILED | Ask the user to try again with a different document. | 
| CHIP_SIGNATURE_VERIFICATION_FAILED | Ask the user to try again with a different document. | 
| CHIP_CSCA_VERIFICATION_FAILED | Ask the user to try again with a different document. | 
{% /table %}

### Not available result

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
| NO_VALID_SUBCHECKS. | Ask the user to try again making sure the data is present on the documents. | 
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