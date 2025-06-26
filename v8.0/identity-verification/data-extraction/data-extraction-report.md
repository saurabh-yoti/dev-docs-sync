---
type: page
title: Report
listed: true
slug: data-extraction-report
description: 
index_title: Report
hidden: 
keywords: 
tags: 
---

Yoti will provide a recommendation for the text data extraction. 

If a manual check is completed please see below for list of recommendation suggestions which will allow you to provide to give the user a correction attempt.

{% table %}
| Recommendation | Yoti score | Description | 
| ---- | ---- | ---- | 
| 🟢  APPROVE | PASS | The data was successfully extracted from the image | 
| 🔴  REJECT | FAIL | The data was not successfully extracted from the image | 
| **🟠** NOT_AVAILABLE | FAIL | Yoti was unable extract the data from the image | 
{% /table %}

As part of the document check, Yoti performs sub checks on the document. The results for the sub checks will be PASS or FAIL. All sub checks state whether the check was performed through a manual process (Expert Review), or through Automation.

{% table widths="184,0" %}
| Sub check | Description | Automated | 
| ---- | ---- | ---- | 
| text_data_readable | If a manual check is completed. This check will always go to our verification centre. It manually verifies that data on the document matches what was extracted automatically and updates if necessary. | ❌ | 
| mrz_validation | This checks that the length of the MRZ data is correct and also checks individual fields, such as the country code, to ensure they are valid. | ✅ | 
{% /table %}

If Yoti was unable to perform checks here is a list of the responses we will return. These may be returned in addition to the reasons listed under the [Document report.](/identity-verification/document-report)

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
- Use our [SDK](https://developers.yoti.com/identity-verification/document-checking#text-extraction).