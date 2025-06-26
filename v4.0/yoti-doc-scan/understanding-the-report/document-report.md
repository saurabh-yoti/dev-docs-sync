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

Yoti performs a numerous amount of sub-checks on the document submitted in order to generate this report request. Yoti will also provide a recommendation for the authenticity of the document:

{% table %}
| Recommendation | Explained | 
| ---- | ---- | 
| APPROVE | The document has passed all of Yoti's checks | 
| REJECT | The document has failed multiple sub-checks | 
| NOT_AVAILABLE | The check was unable to complete. | 
{% /table %}

### Rejection result

For the list of rejection suggestions please see below which will allow you to provide the user a correction attempt:

{% table %}
| Yoti Reason | Description | Recovery suggestions | 
| ---- | ---- | ---- | 
| DOCUMENT_COPY | The user has presented a photocopy of their document, not the original. | Ask the user to try again uploading the original document image. | 
| NO_HOLOGRAM_MOVEMENT | There is no hologram movement detected. | Ask the user to try again on their mobile using their camera. | 
| TAMPERED | The document seems to be tampered with. | You may want to flag this user. | 
| MISSING_HOLOGRAM | There is no expected hologram on the document. | You may want to flag this user. | 
| OTHER_SECURITY_FEATURES | Expected data present or data in correct position checks failed. This will vary document to document.\n\n\n\nAn example of features checked: \n\n\n\nMicroprint, watermarks, optically variable ink, other notable (non-text) features and any visible embossing / engraving. | You may want to flag this user. | 
| EXPIRED_DOCUMENT | The document is past its stated expiry date. | Ask the user to try again with a different document. | 
| FRAUD_LIST_MATCH | The document is present on a list of known frauds. This is only live for the UK. | You may want to flag this user. | 
| DATA_MISMATCH | The document data extracted using OCR and fields extracted from the barcode do not match. | You may want to flag this user. | 
{% /table %}

## Not available result

If Yoti was unable to perform checks here is a list of the responses we will return:

{% table %}
| Yoti Reason | Description | Recovery suggestions | 
| ---- | ---- | ---- | 
| PHOTO_OVEREXPOSED | The photo is overexposed. | Ask the user to try again ensuring no excessive light is on the document. | 
| PHOTO_TOO_DARK | There is not enough ambient light. | Ask the user to try again and move into a lighter area. | 
| PHOTO_TOO_BLURRY | The camera was not held steady or the lens is dirty. | Ask the user to try again with the ID document on a flat surface, or to use their mobile. | 
| DOCUMENT_TOO_DAMAGED | Document is too damaged to the extent where we cannot verify the document. | Ask the user to try again with a different ID document. | 
| GLARE_OBSTRUCTION | Photo is spoilt by a glare from another light source. | Ask the user to try again. | 
| OBJECT_OBSTRUCTION | Object in the way. | Ask the user to try again and ensure you can see the ID fully. | 
| NO_DOCUMENT | The user did not upload a document. | Ask the user to try again and to upload a document. | 
| PARTIAL_PHOTO | The photo is partially taken. | Ask the user to try again and ensure you can see the ID fully. | 
| IMAGE_RESOLUTION_TOO_LOW | The image resolution of the photo is too low. | Ask the user to try again and to use their mobile. | 
| COUNTRY_NOT_SUPPORTED | Documents from this country are not supported. | The user may not be able to complete the process with Yoti. | 
| DOCUMENT_NOT_SUPPORTED | Yoti does not support this document. | Ask the user to try again with a different document. | 
| INCORRECT_DOCUMENT_TYPE | The document type is incorrect. | Ask the user to try again with the correct selected document. | 
| INCORRECT_MRZ | MRZ on passport is incorrect. | Ask the user to try again with a different document. | 
| DOCUMENT_VERSION_NOT_SUPPORTED | Yoti does not support this document template. | Ask the user to try again with a different document. | 
| MISSING_DOCUMENT_SIDE | The front or back of the document was not sent. | Ask the user to try again sending through both sides of the document. | 
| BLACK_AND_WHITE_IMAGE | Black and white photo. | Ask the user to try again with a different document or coloured document. | 
| MISUSE | The photo has been misused. | Ask the user to try again with a different document. | 
| INVALID | The photo is not a valid photo. | Ask the user to try again with a different document. | 
| CHIP_PARSE | NFC chip data was not detected. | Ask the user to try again with a different document. | 
| CHIP_SOD_PARSE | The Security Object Document is not present on the NFC chip data. | Ask the user to try again with a different document. | 
| CHIP_DATA_INTEGRITY_FAILED | Data on NFC fails the integrity check. | You may want to flag this user. | 
| CHIP_SIGNATURE_VERIFICATION_FAILED | Could not verify signature on NFC chip. | You may want to flag this user. | 
| CHIP_CSCA_VERIFICATION_FAILED | Could not verify the Country Signing Certification Authority (CSCA) Certificate on the NFC chip. | Ask the user to try again with a different document. | 
{% /table %}

### Sub Checks explained

As part of the document check, Yoti performs multiple sub checks on the document explained below. The results for the sub checks will be PASS or FAIL.

{% badge type="success" text="Hint: " /%}  Only checks attempted will be shown in the response.

{% table %}
| Sub check | Manual / Automated | Description | 
| ---- | ---- | ---- | 
| DOCUMENT_IN_DATE | Automated | If a valid expiration date is present on the document.\n\nIf this sub check fails, the check will recommend REJECT with a reason of “EXPIRED_DOCUMENT”.\n\nYou must use the text data check for this sub-check to be activated. | 
| FRAUD_LIST_CHECK | Automated | This check will only be returned for UK documents. If this sub check fails, then the overall check will recommend REJECT with a reason of “FRAUD_LIST_MATCH”.\n\nThis check will not be completed for the ROW so you will not see this in your response. | 
| REAL_DOCUMENT | Manual | This sub check is to verify that the original document was used and not a photocopy.\n\nIf this sub check fails, the check will recommend REJECT with a reason of “DOCUMENT_COPY”.\n\n\n\nIf this sub check fails and the document capture method is UPLOAD, then it will not cause the over all check to fail. | 
| EXPECTED_DATA_PRESENT | Manual | If this sub check fails, the over all check recommendation will be REJECT with reason “OTHER_SECURITY_FEATURES” | 
| DATA_IN_CORRECT_POSITION | Manual | Ensuring the data on the document is correctly positioned. If this sub check fails, the over all check recommendation will be REJECT with reason “OTHER_SECURITY_FEATURES” | 
| NO_SIGN_OF_TAMPERING | Manual | If this sub check fails, the over all check recommendation will be REJECT with reason “TAMPERED” | 
| OTHER_SECURITY_FEATURES | Manual | Extra security checks on the document. Ensuring the data on the document is correctly positioned. If this sub check fails, the over all check recommendation will be REJECT with reason “OTHER_SECURITY_FEATURES” | 
| HOLOGRAM | Manual | If this sub check fails, the over all check recommendation will be REJECT with reason “MISSING_HOLOGRAM” | 
| HOLOGRAM_MOVEMENT | Manual | This sub check does not affect the overall recommendation. | 
| CHIP_PARSE | Automated | If chip data is present | 
| CHIP_SOD_PARSE | Automated | If Security Object document is present | 
| CHIP_DATA_INTEGRITY | Automated | Checks the data integrity on the chip | 
| CHIP_DIGITAL_SIGNATURE_VERIFICATION | Automated | Verifies the digital signature and trusth chain | 
| CHIP_CSCA_TRUSTED | Automated | Checks if the  Country Signing Certification Authority (CSCA) Certificate is trusted | 
| OCR_BARCODE_COMPARISON | Automated | This check is performed if fields extracted using OCR from the VIZ (visual inspection zone) of the document and fields extracted from the barcode of a same document both have the mandatory fields populated with values. The entities returned are: Expiration date, date of birth, gender, name, address and document number.\n\n\n\nThis check will only be returned for Canadian Driving licences. | 
| DOC_VALIDATION_NUMBER | Automated | When there is a driving licence where text extraction has been successful (auto or manual) Yoti will attempt to validate the document number. \n\nIf this sub check fails, the overall recommendation will be REJECT with reason DOC_NUMBER_INVALID.\n\n\n\nThis check will only be returned for UK Driving licences. | 
{% /table %}

{% badge type="success" text="Hint: " /%}  Data extraction has to be successful for FRAUD_LIST_CHECK and DOCUMENT_IN_DATE.

---

## Text extraction Report

If this check is successfully performed, the generated media array will contain the extracted text media ID, which can be used to retrieve the JSON object with the extracted data.

This media will replace the "document_fields" media in the resources. 

If machine data extraction is not successful, at session creation there is an option to fallback to manual data extraction. This generates a ‘text data check’ automatically, and the document is reviewed by one of our document processing experts.

Yoti will provide a recommendation for the text data extraction which will contain the sub-check text_data_ readable which will either be a PASS or a FAIL.

{% table %}
| Recommendation | Yoti score | Description | 
| ---- | ---- | ---- | 
| APPROVE | PASS | The data was successfully extracted from the image | 
| REJECT | FAIL | The data was not successfully extracted from the image | 
| NOT_AVAILABLE | FAIL | Yoti was unable extract the data from the image | 
{% /table %}

If a manual check is completed please see below for list of recommendation suggestions which will allow you to provide to give the user a correction attempt:

### Rejection result

{% table %}
| Yoti Response | Description | Recovery suggestion | 
| ---- | ---- | ---- | 
| MRZ_VALIDATION | Yoti checks MRZ data is correct to ensure they are valid. | You may want to flag this user. | 
| CHIP_DATA_INTEGRITY | NFC must be enabled.\n\n\n\nYoti could not validate the document security object using the ICAO certificates | Ask the user to try again with a different document. | 
| CHIP_DIGITAL_SIGNATURE_VERIFICATION | NFC must be enabled.\n\n\n\nIf the verification of the chip failed | Ask the user to try again with a different document. | 
| CHIP_CSCA_TRUSTED | NFC must be enabled.\n\n\n\nIf Yoti do have the root certificate, and fail to verify the chip data against it. | Ask the user to try again with a different document. | 
{% /table %}

### Not available result

{% table %}
| Yoti response | Description | Recovery suggestions | 
| ---- | ---- | ---- | 
| PHOTO_OVEREXPOSED | The photo is overexposed | Ask the user to try again ensuring no excessive light is on the document. | 
| PHOTO_TOO_DARK | There is not enough ambient light. The user needs to move into a lighter frame. | Ask the user to try again and move into a lighter area. | 
| PHOTO_TOO_BLURRY | The camera was not held steady or the lens is dirty. | Ask the user to try again with the ID document on a flat surface, or to use their mobile. | 
| DOCUMENT_TOO_DAMAGED | Document is too damaged (at the point we cannot check) | Ask the user to try again with a different ID document. | 
| GLARE_OBSTRUCTION | There is a glare on the image. | Ask the user to try again. | 
| OBJECT_OBSTRUCTION | Object in the way. | Ask the user to try again and ensure you can see the ID fully. | 
| PARTIAL_PHOTO | The photo is partially taken. | Ask the user to try again and ensure you can see the ID fully. | 
| IMAGE_RESOLUTION_TOO_LOW | The image resolution of the photo is too low. Ask the user to try on their mobile. | Ask the user to try again and to use their mobile. | 
| COUNTRY_NOT_SUPPORTED | Documents from this country are not supported. | The user may not be able to complete the process with Yoti. | 
| DOCUMENT_NOT_SUPPORTED | Yoti does not support this document. | Ask the user to try again with a different document. | 
| INCORRECT_DOCUMENT_TYPE | The document type is incorrect. | Ask the user to try again with the correct selected document. | 
| INCORRECT_MRZ | Machine Readable Zone on passport is incorrect. | Ask the user to try again with a different document. | 
| DOCUMENT_VERSION_NOT_SUPPORTED | Yoti does not support this document type. | Ask the user to try again with a different document. | 
| MISSING_DOCUMENT_SIDE | The front or back of the document was not sent. | Ask the user to try again sending through both sides of the document. | 
| BLACK_AND_WHITE_IMAGE | Yoti does not accept black and white photo's. | Ask the user to try again with a different document or coloured document. | 
| MISUSE | The photo has been misused. | Ask the user to try again with a different document. | 
| INVALID | The photo is not a valid photo. | Ask the user to try again with a different document. | 
| EXTRACTION_FAILED | After being sent for checking if the returned data is sanitised and fails. | Ask the user to try again with a different document. | 
| MRZ_VALIDATION | Yoti checks MRZ data is correct to ensure they are valid. | Ask the user to try again with a different document. | 
| CHIP_PARSE | NFC must be enabled.\n\nYoti could not read the chip. | Ask the user to try again with a different document. | 
| CHIP_SOD_PARSE | NFC must be enabled.\n\nYoti could not read the security object correctly. | Ask the user to try again with a different document. | 
{% /table %}

### Sub Checks explained

As part of the text data check, Yoti performs the following sub check explained below:

{% table %}
| Sub check | Description | 
| ---- | ---- | 
| TEXT_DATA_READABLE | If a manual check is completed. This check will always go to admin. It manually verifies that data on the document matches what was extracted automatically and updates if necessary. | 
{% /table %}

## Document comparison

Document comparison compares values of 2 different documents. This is always done automatically.

If either document is missing both date of birth and name, this check will return NOT_AVAILABLE with reason NO_VALID_SUBCHECKS.

### Rejection result

{% table %}
| Yoti response | Description | Recovery suggestion | 
| ---- | ---- | ---- | 
| MISMATCH | If the date of birth and name does not match. | Ask the user to try again and check their documents have the same attributes. | 
{% /table %}

### Not available result

{% table %}
| Yoti Response | Description | Recovery suggestion | 
| ---- | ---- | ---- | 
| NON_LATIN_CHARACTER_IN_NAME | If the name of the user has a latin character present. | Ask the user to try again with latin characters on their document. | 
{% /table %}

### Sub checks explained

Yoti performs the following sub check explained below which will either be a PASS or a FAIL.

{% table %}
| Sub check | Description | 
| ---- | ---- | 
| DOB_MATCH | If both documents have date of birth, they will be compared. | 
| NAME_MATCH | If both documents have name, they will be compared. | 
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