---
type: page
title: Right to Work / Rent
listed: false
slug: right-to-work---rent
description: 
index_title: Right to Work / Rent
hidden: 
keywords: 
tags: 
---

The JSON below provides an example of the 'identity_profile_requirements' object which is the relevant part of the full request.  This object is the same in the request body for both reusable digital ID (app) and embedded IDV requests.

## Request

{% code %}
{% tab language="json" %}
{
  "trust_framework": "UK_TFIDA",
  "scheme": {
    "type": "RTW"
  }
}
{% /tab %}
{% /code %}

## Response

RTW/R assertion where scheme compliance has been reached.  For clarity the JSON below provides an example of the 'identity_profile' object which is the relevant part of the full response.  This JSON is not full response itself.

### Digital ID Response

This identity profile contains:

- The **identity assertion** required by the RTW/R scheme
- A **verification report** accompanying that assertion, including
    - A boolean to indicate whether RTW/R scheme compliance has been reached overall
    - The GPG45 LoC reached, and the route used to achieve this
    - Detail of the ‘scores’ obtained in each category under GPG45, with links to evidence
    - Evidence details
        - Document evidence, including
            - Links to images of each document (as required by the RTW/R scheme)
            - Fields extracted from each document (this is included for convenience to accompany the images)
            - A high-level description of the checks passed for this evidence

        - Biometric evidence, including
            - A link to the image of the user’s ‘selfie’ (as required by the RTW/R scheme)
            - A description of the liveness method used

- An **authentication report**, including details of which level of authentication was used to authenticate this transaction from the user’s reusable digital ID

{% code %}
{% tab language="json" %}
{
  "identity_assertion": {
    "current_name": {
      "given_names": "JOHN JIM FRED",
      "first_name": "JOHN",
      "middle_name": "JIM FRED",
      "family_name": "FOO",
      "full_name": "JOHN JIM FRED FOO"
    },
    "date_of_birth": "1979-01-01"
  },
  "verification_report": {
    "report_id": "61b99534-116d-4a25-9750-2d708c0fb168",
    "timestamp": "2022-01-02T15:04:05Z",
    "subject_id": "f0726cb6-97c1-4802-9feb-eb7c6cd07949",
    "trust_framework": "UK_TFIDA",
    "schemes_compliance": [
      {
        "scheme": {
          "type": "RTW"
        },
        "requirements_met": true
      }
    ],
    "assurance_process": {
      "level_of_assurance": "MEDIUM",
      "policy": "GPG45",
      "procedure": "M1C",
      "assurance": [
        {
          "type": "EVIDENCE_STRENGTH",
          "classification": "4",
          "evidence_links": [
            "41960172-ca91-487c-8bb3-2c547f80fe54"
          ]
        },
        {
          "type": "EVIDENCE_VALIDITY",
          "classification": "3",
          "evidence_links": [
            "41960172-ca91-487c-8bb3-2c547f80fe54"
          ]
        },
        {
          "type": "VERIFICATION",
          "classification": "3",
          "evidence_links": [
            "41960172-ca91-487c-8bb3-2c547f80fe54",
            "fb0880ca-5dd5-4776-badb-17549123c50b"
          ]
        }
      ]
    },
    "evidence": {
      "documents": [
        {
          "evidence_id": "41960172-ca91-487c-8bb3-2c547f80fe54",
          "timestamp": "2022-01-02T15:04:05Z",
          "document_fields": {
            "full_name": "JOHN JIM FRED FOO",
            "date_of_birth": "1979-01-01",
            "nationality": "GBR",
            "given_names": "JOHN JIM FRED",
            "family_name": "FOO",
            "place_of_birth": "SAMPLETOWN",
            "gender": "MALE",
            "document_type": "PASSPORT",
            "issuing_country": "GBR",
            "document_number": "123456789",
            "expiration_date": "2030-01-01",
            "date_of_issue": "2020-01-01",
            "issuing_authority": "HMPO",
            "mrz": {
              "type": "2",
              "line1": "P<GBRFOO<<JOHN<JIM<FRED<<<<<<<<<<<<<<<<<<<<<",
              "line2": "1234567892GBR7901018M3001215<<<<<<<<<<<<<<02"
            }
          },
          "passed_checks": [
            {
              "check": "CHIP_DIGITAL_SIGNATURE"
            },
            {
              "check": "AUTOMATED_FACE_MATCH"
            },
            {
              "check": "FRAUD_DOCUMENTS_LIST"
            }
          ],
          "verifying_org": "Yoti Ltd.",
          "user_activity_ids": [
            "d4764f67-2992-4a69-9ff4-55b0e77cb3d0"
          ],
          "document_images_attribute_id": "f253c8ab-f07b-4aeb-9dd0-50e670c7ebaf"
        }
      ],
      "face_capture": {
        "evidence_id": "fb0880ca-5dd5-4776-badb-17549123c50b",
        "initial_liveness": {
          "type": "ACTIVE",
          "timestamp": "2022-01-02T15:04:05Z"
        },
        "verifying_org": "Yoti Ltd.",
        "user_activity_ids": [
          "a8e41187-7f5b-4e83-83d5-dc471452f1a8"
        ],
        "selfie_attribute_id": "cc507f84-f1aa-476a-877b-850e949e0fc8"
      }
    }
  },
  "authentication_report": {
    "report_id": "d7202b65-657e-47a7-9679-7596db617b8c",
    "timestamp": "2022-01-02T15:04:05Z",
    "policy": "GPG44",
    "level": "MEDIUM"
  },
  "proof": "<signature provided here>"
}
{% /tab %}
{% /code %}

### IDV Response

This identity profile contains:

- The **identity assertion** required by the RTW/R scheme
- A **verification report** accompanying that assertion, including
    - A boolean to indicate whether RTW/R scheme compliance has been reached overall
    - The GPG45 LoC reached, and the route used to achieve this
    - Detail of the ‘scores’ obtained in each category under GPG45, with links to evidence
    - Evidence details
        - Document evidence, including
            - Links to the IDV resource entity for that evidence (containing media such as document images and extracted fields)
            - Fields extracted from each document (this is included for convenience to accompany the images)
            - Links to relevant checks listed separately, outside the verification report, in the IDV session report for completeness
            - A high-level description of the checks passed for this evidence

        - Biometric evidence, including
            - Links to the IDV resource entity for that evidence (containing media such as face images)
            - Links to relevant checks listed separately, outside the verification report, in the IDV session report for completeness
            - A description of the liveness method used

{% code %}
{% tab language="json" %}
{
  "identity_assertion": {
    "current_name": {
      "given_names": "JOHN JIM FRED",
      "first_name": "JOHN",
      "middle_name": "JIM FRED",
      "family_name": "FOO",
      "full_name": "JOHN JIM FRED FOO"
    },
    "date_of_birth": "1979-01-01"
  },
  "verification_report": {
    "report_id": "61b99534-116d-4a25-9750-2d708c0fb168",
    "timestamp": "2022-01-02T15:04:05Z",
    "subject_id": "f0726cb6-97c1-4802-9feb-eb7c6cd07949",
    "trust_framework": "UK_TFIDA",
    "schemes_compliance": [
      {
        "scheme": {
          "type": "RTW"
        },
        "requirements_met": true
      }
    ],
    "assurance_process": {
      "level_of_assurance": "MEDIUM",
      "policy": "GPG45",
      "procedure": "M1A",
      "assurance": [
        {
          "type": "EVIDENCE_STRENGTH",
          "classification": "4",
          "evidence_links": [
            "41960172-ca91-487c-8bb3-2c547f80fe54"
          ]
        },
        {
          "type": "EVIDENCE_VALIDITY",
          "classification": "2",
          "evidence_links": [
            "41960172-ca91-487c-8bb3-2c547f80fe54"
          ]
        },
        {
          "type": "IDENTITY_FRAUD",
          "classification": "1",
          "evidence_links": [
            "db3d1991-7dcc-4a84-b9f5-26becd8f25de"
          ]
        },
        {
          "type": "VERIFICATION",
          "classification": "3",
          "evidence_links": [
            "41960172-ca91-487c-8bb3-2c547f80fe54",
            "fb0880ca-5dd5-4776-badb-17549123c50b"
          ]
        }
      ]
    },
    "evidence": {
      "documents": [
        {
          "evidence_id": "41960172-ca91-487c-8bb3-2c547f80fe54",
          "timestamp": "2022-01-02T15:04:05Z",
          "document_fields": {
            "full_name": "JOHN JIM FRED FOO",
            "date_of_birth": "1979-01-01",
            "nationality": "GBR",
            "given_names": "JOHN JIM FRED",
            "family_name": "FOO",
            "place_of_birth": "SAMPLETOWN",
            "gender": "MALE",
            "document_type": "PASSPORT",
            "issuing_country": "GBR",
            "document_number": "123456789",
            "expiration_date": "2030-01-01",
            "date_of_issue": "2020-01-01",
            "issuing_authority": "HMPO",
            "mrz": {
              "type": "2",
              "line1": "P<GBRFOO<<JOHN<JIM<FRED<<<<<<<<<<<<<<<<<<<<<",
              "line2": "1234567892GBR7901018M3001215<<<<<<<<<<<<<<02"
            }
          },
          "passed_checks": [
            {
              "check": "MANUAL_VISUAL_DOCUMENT_AUTHENTICITY"
            },
            {
              "check": "AUTOMATED_FACE_MATCH"
            },
            {
              "check": "FRAUD_DOCUMENTS_LIST"
            }
          ],
          "resource_ids": [
            "<links to the IDV resource id(s) for this document>"
          ],
          "check_ids": [
            "<links to relevant checks in the IDV report>"
          ],
          "verifying_org": "Yoti Ltd."
        }
      ],
      "face_capture": {
        "evidence_id": "fb0880ca-5dd5-4776-badb-17549123c50b",
        "initial_liveness": {
          "type": "ZOOM",
          "timestamp": "2022-01-02T15:04:05Z"
        },
        "verifying_org": "Yoti Ltd.",
        "resource_ids": [
          "<links to any relevant IDV resource id(s) for this check>"
        ],
        "check_ids": [
          "<links to relevant checks in the IDV report where applicable>"
        ]
      },
      "electronic_records": [
        {
          "evidence_id": "db3d1991-7dcc-4a84-b9f5-26becd8f25de",
          "timestamp": "2022-01-02T15:04:05Z",
          "identity_details": {
            "full_name": "JON JIM FRED FOO",
            "given_names": "JON JIM FRED",
            "family_name": "FOO",
            "date_of_birth": "1979-01-01"
          },
          "verifying_org": "Yoti Ltd.",
          "provider_org": "Cifas Ltd.",
          "resource_ids": [
            "<links to any relevant IDV resource id(s) for this check>"
          ],
          "check_ids": [
            "<links to relevant checks in the IDV report where applicable>"
          ]
        }
      ]
    }
  },
  "proof": "<signature provided here>"
}
{% /tab %}
{% /code %}

Note that, outside the “identity profile” object given above, the IDV session report will also include details of all evidence that was captured, checks performed etc. for completeness.

Elements of the identity profile verification report link to relevant checks and resources, for ease of reference.