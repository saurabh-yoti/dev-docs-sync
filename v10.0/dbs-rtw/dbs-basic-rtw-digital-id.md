---
type: page
title: DBS Basic and RTW
listed: true
slug: dbs-basic-rtw-digital-id
description: 
index_title: DBS Basic and RTW
hidden: 
keywords: 
tags: 
---

For clarity the JSON below provides an example of the 'identity-profile-requirements' object which is the relevant part of the full request. 

## Request

{% code %}
{% tab language="json" %}
{
  "trust_framework": "UK_TFIDA",
  "scheme": {
    "type": "DBS_RTW",
    "objective": "BASIC"
  }
}
{% /tab %}
{% /code %}

## Response

An assertion which meets both the DBS Basic and RTW scheme requirements, where scheme compliance has been reached.  For clarity the JSON below provides an example of the 'identity profile' object which is the relevant part of the full response.  This JSON is not full response itself.

This example is very similar to the DBS Basic example above, because a GBR Passport is used in both cases.  The main difference here is that the attribute IDs for document images and the ‘selfie’ of the user are also included, as required by the RTW scheme.  In addition, there are now two scheme compliance reports: one for DBS Basic, and one for RTW.

### Digital ID response

This identity profile contains:

- The **identity assertion** required by the DBS and RTW/R schemes (the union of the two sets)
- A **verification report** accompanying that assertion, including
    - A boolean to indicate whether DBS scheme compliance has been reached overall, for the level of DBS check (objective) requested
    - A boolean to indicate whether RTW/R scheme compliance has been reached overall
    - The GPG45 LoC reached, and the route used to achieve this
    - Detail of the ‘scores’ obtained in each category under GPG45, with links to evidence
    - Evidence details
        - Document evidence, including
            - Links to images of each document (as required by the RTW/R scheme)
            - Fields extracted from each document (to satisfy the DBS scheme requirement for Passport and Driving Licence details)
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
    "date_of_birth": "1979-01-01",
    "current_address": {
      "address": {
        "address_format": "1",
        "building_number": "107",
        "address_line1": "107 LEADENHALL STREET",
        "address_line2": "LONDON",
        "address_line3": "EC3A 4AF",
        "town_city": "LONDON",
        "postal_code": "EC3A 4AF",
        "country_iso": "GBR",
        "country": "United Kingdom",
        "formatted_address": "107 LEADENHALL STREET, LONDON, EC3A 4AF"
      }
    }
  },
  "verification_report": {
    "address_verification": {
      "current_address_verified": true,
      "evidence_links": [
        "73b78f41-a158-4b23-a66e-a712d2820edb"
      ]
    },
    "report_id": "61b99534-116d-4a25-9750-2d708c0fb168",
    "timestamp": "2022-01-02T15:04:05Z",
    "subject_id": "f0726cb6-97c1-4802-9feb-eb7c6cd07949",
    "trust_framework": "UK_TFIDA",
    "schemes_compliance": [
      {
        "scheme": {
          "type": "DBS",
          "objective": "BASIC"
        },
        "requirements_met": true
      },
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
          "document_images_attribute_id": "f253c8ab-f07b-4aeb-9dd0-50e670c7ebaf",
          "user_activity_ids": [
            "d4764f67-2992-4a69-9ff4-55b0e77cb3d0"
          ]
        }
      ],
      "face_capture": {
        "evidence_id": "fb0880ca-5dd5-4776-badb-17549123c50b",
        "initial_liveness": {
          "type": "ACTIVE",
          "timestamp": "2022-01-02T15:04:05Z"
        },
        "verifying_org": "Yoti Ltd.",
        "selfie_attribute_id": "cc507f84-f1aa-476a-877b-850e949e0fc8",
        "user_activity_ids": [
          "a8e41187-7f5b-4e83-83d5-dc471452f1a8"
        ]
      },
      "electronic_records": [
        {
          "evidence_id": "73b78f41-a158-4b23-a66e-a712d2820edb",
          "timestamp": "2022-01-02T15:04:05Z",
          "identity_details": {
            "full_name": "JON JIM FRED FOO",
            "given_names": "JON JIM FRED",
            "family_name": "FOO",
            "date_of_birth": "1979-01-01",
            "structured_postal_address": {
              "address_format": "1",
              "building_number": "107",
              "address_line1": "107 LEADENHALL STREET",
              "address_line2": "LONDON",
              "address_line3": "EC3A 4AF",
              "town_city": "LONDON",
              "postal_code": "EC3A 4AF",
              "country_iso": "GBR",
              "country": "United Kingdom",
              "formatted_address": "107 LEADENHALL STREET, LONDON, EC3A 4AF"
            }
          },
          "verifying_org": "Yoti Ltd.",
          "provider_org": "TransUnion Ltd.",
          "user_activity_ids": [
            "fa315acb-4d8c-4886-815d-775c882aa448"
          ]
        }
      ]
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