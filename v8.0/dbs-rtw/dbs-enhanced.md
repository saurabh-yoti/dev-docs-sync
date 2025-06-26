---
type: page
title: DBS Enhanced
listed: false
slug: dbs-enhanced
description: 
index_title: DBS Enhanced
hidden: 
keywords: 
tags: 
---

For clarity the JSON below provides an example of the 'identity_profile_requirements' object which is the relevant part of the full request.  This object is the same in the request body for both reusable digital ID (app) and embedded IDV requests.

Request

{% code %}
{% tab language="json" %}
{
  "trust_framework": "UK_TFIDA",
  "scheme": {
    "type": "DBS",
    "objective": "ENHANCED"
  }
}
{% /tab %}
{% /code %}

Response

DBS Enhanced assertion where scheme compliance has been reached.  For clarity the JSON below provides an example of the 'identity profile' object which is the relevant part of the full response.  This JSON is not full response itself.

Digital ID response

This identity profile contains:

- The **identity assertion** required by the DBS scheme
- A **verification report** accompanying that assertion, including
    - A boolean to indicate whether DBS scheme compliance has been reached overall, for the level of DBS check (objective) requested
    - The GPG45 LoC reached, and the route used to achieve this
    - Detail of the ‘scores’ obtained in each category under GPG45, with links to evidence
    - Evidence details
        - Document evidence, including
            - Fields extracted from each document (to satisfy the DBS scheme requirement for Passport and Driving Licence details)
            - A high-level description of the checks passed for this evidence

        - Biometric evidence, including
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
        "6c5e27f5-6928-483d-8c01-90a551374474",
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
          "objective": "ENHANCED"
        },
        "requirements_met": true
      }
    ],
    "assurance_process": {
      "level_of_assurance": "HIGH",
      "policy": "GPG45",
      "procedure": "H2B",
      "assurance": [
        {
          "type": "EVIDENCE_STRENGTH",
          "classification": "4",
          "evidence_links": [
            "41960172-ca91-487c-8bb3-2c547f80fe54"
          ]
        },
        {
          "type": "EVIDENCE_STRENGTH",
          "classification": "3",
          "evidence_links": [
            "6c5e27f5-6928-483d-8c01-90a551374474"
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
          "type": "EVIDENCE_VALIDITY",
          "classification": "3",
          "evidence_links": [
            "6c5e27f5-6928-483d-8c01-90a551374474"
          ]
        },
        {
          "type": "IDENTITY_FRAUD",
          "classification": "2",
          "evidence_links": [
            "db3d1991-7dcc-4a84-b9f5-26becd8f25de",
            "73b78f41-a158-4b23-a66e-a712d2820edb"
          ]
        },
        {
          "type": "VERIFICATION",
          "classification": "3",
          "evidence_links": [
            "41960172-ca91-487c-8bb3-2c547f80fe54",
            "6c5e27f5-6928-483d-8c01-90a551374474",
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
          ]
        },
        {
          "evidence_id": "6c5e27f5-6928-483d-8c01-90a551374474",
          "timestamp": "2022-01-02T15:04:05Z",
          "document_fields": {
            "full_name": "JOHN JIM FRED FOO",
            "date_of_birth": "1979-01-01",
            "nationality": "GBR",
            "given_names": "JOHN JIM FRED",
            "family_name": "FOO",
            "place_of_birth": "SAMPLE COUNTRY",
            "gender": "MALE",
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
            },
            "document_type": "DRIVING_LICENCE",
            "issuing_country": "GBR",
            "document_number": "FOO99701011JJ9ZM13",
            "expiration_date": "2030-01-01",
            "date_of_issue": "2020-01-01",
            "issuing_authority": "DVLA"
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
          "verifying_org": "Yoti Ltd.",
          "user_activity_ids": [
            "b37ed6e0-6da9-41dd-a7b4-edae52eddf75"
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
        "user_activity_ids": [
          "a8e41187-7f5b-4e83-83d5-dc471452f1a8"
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
          "provider_org": "Cifas Ltd.",
          "user_activity_ids": [
            "839a36e9-744e-4b92-8a24-6164a5aca2aa"
          ]
        },
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

IDV response

This identity profile contains:

- The **identity assertion** required by the DBS scheme
- A **verification report** accompanying that assertion, including
    - A boolean to indicate whether DBS scheme compliance has been reached overall, for the level of DBS check (objective) requested
    - The GPG45 LoC reached, and the route used to achieve this
    - Detail of the ‘scores’ obtained in each category under GPG45, with links to evidence
    - Evidence details
        - Document evidence, including
            - Fields extracted from each document (to satisfy the DBS scheme requirement for Passport and Driving Licence details)
            - Links to the IDV resource entity for that evidence (containing media such as document images and extracted fields)
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
        "6c5e27f5-6928-483d-8c01-90a551374474",
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
          "objective": "ENHANCED"
        },
        "requirements_met": true
      }
    ],
    "assurance_process": {
      "level_of_assurance": "HIGH",
      "policy": "GPG45",
      "procedure": "H2B",
      "assurance": [
        {
          "type": "EVIDENCE_STRENGTH",
          "classification": "4",
          "evidence_links": [
            "41960172-ca91-487c-8bb3-2c547f80fe54"
          ]
        },
        {
          "type": "EVIDENCE_STRENGTH",
          "classification": "3",
          "evidence_links": [
            "6c5e27f5-6928-483d-8c01-90a551374474"
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
          "type": "EVIDENCE_VALIDITY",
          "classification": "3",
          "evidence_links": [
            "6c5e27f5-6928-483d-8c01-90a551374474"
          ]
        },
        {
          "type": "IDENTITY_FRAUD",
          "classification": "2",
          "evidence_links": [
            "db3d1991-7dcc-4a84-b9f5-26becd8f25de",
            "73b78f41-a158-4b23-a66e-a712d2820edb"
          ]
        },
        {
          "type": "VERIFICATION",
          "classification": "3",
          "evidence_links": [
            "41960172-ca91-487c-8bb3-2c547f80fe54",
            "6c5e27f5-6928-483d-8c01-90a551374474",
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
          "verifying_org": "Yoti Ltd.",
          "resource_ids": [
            "<links to the IDV resource id(s) for this document>"
          ],
          "check_ids": [
            "<links to relevant checks in the IDV report>"
          ]
        },
        {
          "evidence_id": "6c5e27f5-6928-483d-8c01-90a551374474",
          "timestamp": "2022-01-02T15:04:05Z",
          "document_fields": {
            "full_name": "JOHN JIM FRED FOO",
            "date_of_birth": "1979-01-01",
            "nationality": "GBR",
            "given_names": "JOHN JIM FRED",
            "family_name": "FOO",
            "place_of_birth": "SAMPLE COUNTRY",
            "gender": "MALE",
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
            },
            "document_type": "DRIVING_LICENCE",
            "issuing_country": "GBR",
            "document_number": "FOO99701011JJ9ZM13",
            "expiration_date": "2030-01-01",
            "date_of_issue": "2020-01-01",
            "issuing_authority": "DVLA"
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
          "verifying_org": "Yoti Ltd.",
          "resource_ids": [
            "<links to the IDV resource id(s) for this document>"
          ],
          "check_ids": [
            "<links to relevant checks in the IDV report>"
          ]
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
          "<links to the IDV resource id(s) for this document>"
        ],
        "check_ids": [
          "<links to relevant checks in the IDV report>"
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
          "provider_org": "Cifas Ltd.",
          "resource_ids": [
            "<links to the IDV resource id(s) for this document>"
          ],
          "check_ids": [
            "<links to relevant checks in the IDV report>"
          ]
        },
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
          "resource_ids": [
            "<links to the IDV resource id(s) for this document>"
          ],
          "check_ids": [
            "<links to relevant checks in the IDV report>"
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