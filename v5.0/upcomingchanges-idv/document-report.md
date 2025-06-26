---
type: page
title: Document report
listed: false
slug: document-report
description: 
index_title: Document report
hidden: 
keywords: 
tags: 
---

Yoti is constantly evolving the Identity verification service. 

We have been busy testing new document processing frameworks, based on client feedback and internal analysis. We are making some changes to our manual document authenticity checks and responses which we would like to make you aware of. 

To review the current document report head over [here](https://developers.yoti.com/identity-verification/document-report). 

**GO LIVE DATE:**  5th July 2021

---

### Key

{% badge type="info" text="NEW" /%} Introducing a NEW value.

{% badge type="warning" text="CHANGE" /%} There has been a CHANGE in the value.

---

## Document report

Yoti performs numerous checks on a document in order to generate this report. Yoti will also provide a recommendation for the authenticity of the document:

{% table %}
| Recommendation | Explained | 
| ---- | ---- | 
| APPROVE | The document has passed Yoti verification standards. | 
| REJECT | The document could be tampered or a counterfeit. Yoti recommends you flag users that are rejected. | 
| NOT_AVAILABLE | Yoti couldn’t perform the check, usually due to the quality of submitted images or user error. | 
{% /table %}

### Sub checks

As part of the document check, Yoti performs multiple sub checks on the document explained below. The outcome for these will either be PASS or FAIL.

{% badge type="success" text="Hint" /%} Only checks attempted will be shown in the response.

{% table widths="206,214,111" %}
| Sub check | Description | Automated | Rejection result | 
| ---- | ---- | ---- | ---- | 
| {% badge type="info" text="NEW" /%}no_signs_of_forgery | Yoti has added a new check, where we will assess multiple features of the document to include a wider range of checks. | No | {% badge type="info" text="NEW" /%} COUNTERFEIT \n\n\n\nYoti will provide a PASS / FAIL breakdown with respective detail on:\n\n\n\n- data_alignment\n- hologram_check\n- security_features_integrity\n- printing_quality\n- fonts_authenticity\n- document_number_integrity | 
| document_in_date | If a valid expiration date is present on the document. | Yes | EXPIRED_DOCUMENT | 
| fraud_list_check | Yoti will check a fraudulent document database for a match. | Yes | FRAUD_LIST MATCH | 
| {% badge type="warning" text="CHANGE" /%} real_document. will be updated to: physical_document_captured | This sub check is to verify that the original document was used and not a photocopy. | No | DOCUMENT_COPY | 
| no_sign_of_tampering | If Yoti does detect a tampered document we will highlight where. | No | {% badge type="info" text="NEW" /%}\n\nTAMPERED with PASS / FAIL breakdown:\n\n\n\n- face_photo\n- data\n- both | 
| other_security_features | Extra security checks on the document. \n\n\n\nMicroprint, watermarks, optically variable ink, other notable (non-text) features and any visible embossing / engraving.\n\n\n{% badge type="warning" text="CHANGE" /%} no longer results in a rejection recommendation. | No | N/A | 
| hologram | Yoti will detect if we can see a shape / colour of the hologram. \n\n\n\n{% badge type="warning" text="CHANGE" /%} no longer results in a rejection recommendation. | No | N/A | 
| hologram_movement | Check hologram movement. | No | N/A | 
| ocr_barcode_comparison | This check is performed if fields extracted using OCR from the VIZ (visual inspection zone) of the document and fields extracted from the barcode of a same document both have the mandatory fields populated with values. | Yes | DATA_MISMATCH\n\nThe document data extracted using OCR and fields extracted from the barcode do not match.\n\n\n\nThe entities returned are:\n\n\n\n- expiration date\n- date of birth\n- gender\n- name\n- address\n- document number. | 
| doc_validation_number | When there is a driving licence where text extraction has been successful (auto or manual) Yoti will attempt to validate the document number.\n\n\n\nThis check will only be returned for UK Driving licences and Canadian licences (Ontario, Newfoundland and Quebec) | Yes | DOC_NUMBER_INVALID | 
{% /table %}

Note: No changes have been made to NFC responses for native mobile integrations.