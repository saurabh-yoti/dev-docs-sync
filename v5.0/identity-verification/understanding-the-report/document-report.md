---
type: page
title: Document report
listed: true
slug: document-report
description: 
index_title: Document report
hidden: 
keywords: 
tags: 
---

Yoti performs numerous checks on a document in order to generate this report. Yoti will also provide a recommendation for the authenticity of the document:

{% table %}
| Recommendation | Explained | 
| ---- | ---- | 
| APPROVE | The document has passed Yoti verification standards. | 
| REJECT | The document could be tampered or a counterfeit. Yoti recommends you flag users that are rejected. | 
| NOT_AVAILABLE | Yoti couldn’t perform the check, usually due to the quality of submitted images or user error. | 
{% /table %}

As part of the document check, Yoti performs multiple sub checks on the document explained below. The results for the sub checks will be PASS or FAIL.

{% badge type="success" text="Hint: " /%} Only checks attempted will be shown in the response.

{% table widths="165,250,0" %}
| Sub check | Description | Automated | Result | 
| ---- | ---- | ---- | ---- | 
| no_signs_of_forgery | Yoti will assess multiple features of the document to include a wider range of checks. | ❌ | COUNTERFEIT \n\n\n\nYoti will provide a PASS / FAIL breakdown with respective detail on:\n\n\n\n- data_alignment\n- hologram_check\n- security_features_integrity\n- printing_quality\n- fonts_authenticity\n- document_number_integrity | 
| document_in_date | If a valid expiration date is present on the document. | ✅ | EXPIRED_DOCUMENT | 
| fraud_list_check | Yoti will check a fraudulent document database for a match. | ✅ | FRAUD_LIST MATCH | 
| real_document \n\n\n\n{% badge type="warning" text="CHANGE" /%} 15th July.\n\nThis will be updated to: physical_document_captured | This sub check is to verify that the original document was used and not a photocopy. | ❌ | DOCUMENT_COPY | 
| no_sign_of_tampering | If Yoti does detect a tampered document we will highlight where. | ❌ | TAMPERED with PASS / FAIL breakdown:\n\n\n\n- face_photo\n- data\n- both | 
| hologram | Yoti will detect if we can see a shape / colour of the hologram. | ❌ | Yoti will provide a PASS / FAIL breakdown. | 
| hologram_movement | Check hologram movement. | ❌ | Yoti will provide a PASS / FAIL breakdown. | 
| ocr_barcode_comparison | This check is performed if fields extracted using OCR from the VIZ (visual inspection zone) of the document and fields extracted from the barcode of a same document both have the mandatory fields populated with values. | ✅ | DATA_MISMATCH \n\n\n\nThe document data extracted using OCR and fields extracted from the barcode do not match.\n\n\n\nThe entities returned are:\n\n\n\n- expiration date\n- date of birth\n- gender\n- name\n- address\n- document number. | 
| doc_number_validation | When there is a driving licence where text extraction has been successful (auto or manual) Yoti will attempt to validate the document number.\n\n\n\nThis check will only be returned for UK Driving licences and Canadian licences (Ontario, Newfoundland and Quebec) | ✅ | DOC_NUMBER_INVALID | 
| chip_parse | If chip data is present | ✅ | CHIP_PARSE | 
| chip_sod_parse | If Security Object document is present | ✅ | CHIP_SOD_PARSE | 
| chip_data_integrity | Checks the data integrity on the chip | ✅ | CHIP_DATA_INTEGRITY_FAILED | 
| chip_digital_\n\nsignature_verification | Verifies the digital signature and trust chain | ✅ | CHIP_SIGNATURE_\n\nVERIFICATION_FAILED | 
| chip_csca_trusted | Checks if the Country Signing Certification Authority (CSCA) Certificate is trusted | ✅ | CHIP_CSCA_\n\nVERIFICATION_FAILED | 
{% /table %}

Rejection result

For the list of rejection suggestions please see below which will allow you to provide the user a correction attempt:

{% table %}
| Yoti Reason | Recovery suggestions | 
| ---- | ---- | 
| COUNTERFEIT | You may want to flag this user. | 
| EXPIRED_DOCUMENT | Ask the user to try again with a different document. | 
| FRAUD_LIST_MATCH | You may want to flag this user. | 
| DOCUMENT_COPY | Ask the user to try again with the original document. | 
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

## Text extraction Report

If this check is successfully performed, the generated media array will contain the extracted text media ID, which can be used to retrieve the JSON object with the extracted data.

This media will replace the "document_fields" media in the resources. 

If machine data extraction is not successful, at session creation there is an option to fallback to manual data extraction. This generates a ‘text data check’ automatically, and the document is reviewed by one of our document processing experts.

Yoti will provide a recommendation for the text data extraction which will contain the sub-check text_data_  readable which will either be a PASS or a FAIL.

If a manual check is completed please see below for list of recommendation suggestions which will allow you to provide to give the user a correction attempt.

{% table %}
| Recommendation | Yoti score | Description | 
| ---- | ---- | ---- | 
| APPROVE | PASS | The data was successfully extracted from the image | 
| REJECT | FAIL | The data was not successfully extracted from the image | 
| NOT_AVAILABLE | FAIL | Yoti was unable extract the data from the image | 
{% /table %}

Yoti will provide a recommendation for the text data extraction which will contain the sub-check text_data_  readable which will either be a PASS or a FAIL:

{% table widths="184,0,112" %}
| Sub check | Description | Automated | Result | 
| ---- | ---- | ---- | ---- | 
| text_data_readable | If a manual check is completed. This check will always go to our verification centre. It manually verifies that data on the document matches what was extracted automatically and updates if necessary. | ❌ | Yoti will provide a PASS / FAIL breakdown. | 
| mrz_validation | This checks that the length of the MRZ data is correct and also checks individual fields, such as the country code, to ensure they are valid. | ✅ | Yoti will provide a PASS / FAIL breakdown. | 
{% /table %}

### Not available result

If Yoti was unable to perform checks here is a list of the responses we will return:

{% table %}
| Yoti response | Description | Recovery suggestions | 
| ---- | ---- | ---- | 
| EXTRACTION_FAILED | After being sent for checking if the returned data is sanitised and fails. | Ask the user to try again with a different document. | 
| MRZ_VALIDATION | Yoti checks MRZ data is correct to ensure they are valid. | Ask the user to try again with a different document. | 
{% /table %}

---

## Document comparison

Document comparison compares values of 2 different documents. This is always done automatically.

Yoti performs the following sub check explained below which will either be a PASS or a FAIL.

{% table %}
| Sub check | Description | Automated | Result | 
| ---- | ---- | ---- | ---- | 
| dob_match | If both documents have date of birth, they will be compared. | ✅ | MISMATCH | 
| name_match | If both documents have name, they will be compared. | ✅ | MISMATCH / NON_LATIN_CHARACTER_IN_NAME. | 
{% /table %}

### Rejection result

For the list of rejection suggestions please see below which will allow you to provide the user a correction attempt:

{% table %}
| Yoti response | Recovery suggestion | 
| ---- | ---- | 
| MISMATCH | Ask the user to try again and check their documents have the same attributes. | 
{% /table %}

### Not available result

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
       Note
    </div>
    <div class="alert-text">
For Supported documents we will complete a NAME comparison. For two ID documents we will do a DOB and a NAME comparison.    </div>
    <div class="alert-links"> 
   </div>
</div>
{% /html %}