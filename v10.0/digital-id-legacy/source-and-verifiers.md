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

---

## Add a constraint

On the Digital ID, the document the user adds last will default to be the source of the attributes shared. If you wish to ensure your attributes have come from a specific source please follow the below instructions:

1. Log on to the [**Yoti Hub**](https://hub.yoti.com/login)
2. Head over to your application and scenario.
3. Go to the bottom and you will see advanced settings:

{% image url="https://uploads.developerhub.io/prod/kvAX/1jivz1bo0rmltsf2p3oip15qv7100lnj2svfg7l6m6894x1w5lkszooie79qovbd.png" caption="Application &gt; Scenario &gt; Advanced settings" mode="300" height="1070" width="940" %}
{% /image %}

4. Click advanced policy editor.
5. Find the attributes you want with a source constraint and add an anchor source. See below for an example with a full name and date of birth.

{% code %}
{% tab language="json" %}
{
          constraints: [
            {
              type: 'SOURCE',
              preferred_sources: {
                anchors: [
                  {
                    name: 'PASSPORT',
                    sub_type: ''
                  }
                ],
                soft_preference: false
              }
            }
          ],
          name: 'date_of_birth',
          anchors: [],
          derivation: '',
          optional: false,
          accept_self_asserted: false,
          alternative_names: []
        },
        {
          constraints: [
            {
              type: 'SOURCE',
              preferred_sources: {
                anchors: [
                  {
                    name: 'PASSPORT',
                    sub_type: ''
                  }
                ],
                soft_preference: false
              }
            }
          ],
          name: 'full_name',
          anchors: [],
          derivation: '',
          optional: false,
          accept_self_asserted: false,
          alternative_names: []
        }
{% /tab %}
{% /code %}