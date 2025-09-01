---
type: page
title: Source and verifiers
listed: true
slug: source-and-verifiers
description: 
index_title: Source and verifiers
hidden: 
keywords: 
tags: 
---

Within the SDKs and in our Yoti Hub you can see the sources and verifiers of each of the attributes the user has shared with your company.

Below represents an explanation of what is shown through our SDKs.

## Sources

{% table %}
| Value | Description | Possible subtypes | 
| ---- | ---- | ---- | 
| USER_PROVIDED | Indicates that this attribute value was self-asserted by the user, with no supporting document as proof. | DAY_MONTH | 
| PASSPORT | Indicates that this attribute value was extracted from a passport.\n\n\n\nThe two subtypes available are via:- OCR or NFC. | OCR, NFC | 
| DRIVING_LICENCE | Indicates that this attribute value was extracted from a driving licence. | N/A | 
| NATIONAL_ID | The attribute was extracted from a National ID card / document | AADHAAR, STATE_ID, MYKAD | 
| PASS_CARD | The attribute was extracted from a PASS card/document. | CITIZENCARD | 
{% /table %}

## Verifiers

{% table %}
| Value | Description | 
| ---- | ---- | 
| YOTI_ADMIN | Indicates that this attribute value has been manually checked by staff at the Yoti security centre. | 
| YOTI_IDENTITY | Indicates that the attribute value has been verified with a recognised identity database, or otherwise known as an Identity Verifier (IDV). | 
| YOTI_OTP | The attribute has been verified by sending a generated one time passcode to it and checking it has been received | 
| PASSPORT_NFC_SIGNATURE | The attribute was verified by its passport NFC signature | 
| YOTI_UIDAI | Indicates that the attribute value has been verified with the Indian UIDAI system. | 
| ISSUING_AUTHORITY | The attribute has been verified with a recognised document database | 
| ISSUING_AUTHORITY_PKI | The signature that signed over the value on the original document has been verified with the relevant certificate authority | 
{% /table %}