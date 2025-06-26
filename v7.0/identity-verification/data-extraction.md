---
type: page
title: Data extraction
listed: true
slug: data-extraction
description: 
index_title: Data extraction
hidden: 
keywords: 
tags: 
---

If you wish to request the document details from the user this section will provide you context on what this check entails. 

This section will describe:

- What a data extraction check is
- Rejection results
- Not available results

---

## Data extraction check

If machine data extraction is not successful, at session creation there is an option to fallback to manual data extraction. This generates a ‘text data check’ automatically, and the document is reviewed by one of our document processing experts.

Yoti will attempt to extract as much as data as possible depending on the document type. 

- Full Name
- Date of birth in the form yyyy-mm-dd.
- Nationality is the nationality expressed as an ISO/ICAO alpha-3 country code.
- Given Names contains first and middle names.
- First Name
- Middle Name
- FamilyName is the family name.
- Place of birth - it may contain a country name or a city name or both.
- Country of birth
- Gender is the gender and can be any of the following values: "MALE", "FEMALE", "TRANSGENDER" or "OTHER".
- NamePrefix 
- First name alias
- Middle name alias
- Family name alias
- Weight
- Height
- Eye colour
- Structured postal address
- Document Type
- Issuing Country - Defined as an ISO/ICAO alpha-3 country code.
- DocumentNumber
- Expiration Date in the form yyyy-mm-dd. This will return LIFETIME if the document has LIFETIME as a expiry time.
- Date of issue
- Issuing Authority
- MRZ data as displayed on the document

If the document has an MRZ or a barcode, Yoti will attempt a comparison.

---

## The results

Yoti will provide a recommendation for the text data extraction which will contain the sub-check text_data_ readable which will either be a PASS or a FAIL.

If a manual check is completed please see below for list of recommendation suggestions which will allow you to provide to give the user a correction attempt.

{% table %}
| Recommendation | Yoti score | Description | 
| ---- | ---- | ---- | 
| APPROVE 🟢 | PASS | The data was successfully extracted from the image | 
| REJECT 🔴 | FAIL | The data was not successfully extracted from the image | 
| NOT_AVAILABLE 🟠 | FAIL | Yoti was unable extract the data from the image | 
{% /table %}

Yoti will provide a recommendation for the text data extraction which will contain the sub-check text_data_readable which will either be a PASS or a FAIL:

{% table widths="184,0" %}
| Sub check | Description | Automated | 
| ---- | ---- | ---- | 
| text_data_readable | If a manual check is completed. This check will always go to our verification centre. It manually verifies that data on the document matches what was extracted automatically and updates if necessary. | ❌ | 
| mrz_validation | This checks that the length of the MRZ data is correct and also checks individual fields, such as the country code, to ensure they are valid. | ✅ | 
{% /table %}

If Yoti was unable to perform checks here is a list of the responses we will return:

{% table %}
| Yoti response | Description | Recovery suggestions | 
| ---- | ---- | ---- | 
| EXTRACTION_FAILED | After being sent for checking if the returned data is sanitised and fails. | Ask the user to try again with a different document. | 
| MRZ_VALIDATION | Yoti checks MRZ data is correct to ensure they are valid. | Ask the user to try again with a different document. | 
{% /table %}

---

## Request data extraction check

If you would like to request this check you can in two ways:

- Use our [portal](https://developers.yoti.com/identity-verification/portal-guide#request-text-extraction-task).
- Use our [SDK](https://developers.yoti.com/identity-verification/document-checking#text-extraction) or [API](https://yoti.world/yoti-public-api/#/Backend%20Endpoints/post_sessions).