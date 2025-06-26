---
type: page
title: Session retrieval
listed: true
slug: session-retrieval
description: 
index_title: Session retrieval
hidden: 
keywords: 
tags: 
---

The response from this endpoint will detail all information, check and task completion status, resource and media data, along with the associated media identifiers. The session will only detail the requested check and tasks from the create session request. 

Sessions can be retrieved at any time, however the integrating backend will be notified when a session update occurs, according to the "notifications" settings provided at session creation.

**Base URL**: Please contact Yoti for this on [sdksupport@yoti.com](mailto:sdksupport@yoti.com)

Request authentication will be required. Full details for the required authorisation headers can be found [here](/yoti-doc-scan/authentication-and-headers).

{% table %}
| Endpoint | 
| ---- | 
| GET /idverify/v1/sessions/{session_id}?sdkId={sdkId}&amp;nonce={nonce}&amp;timestamp={timestamp} | 
{% /table %}

{% table %}
| Parameter | Description | Example | 
| ---- | ---- | ---- | 
| session_id | The session id obtained from the generate session request | 9d539c59-1cd0-4e2c-bed8-eb525248aa84 | 
| sdkId | The SDK ID from your Yoti Hub | b3c6bed3-8f17-46b1-a008-3aebc2da0b79 | 
| nonce | Unique ID for this request transaction. This should be in GUID form and should be uniquely generated for each request.&nbsp; | 24487c75-0d20-457f-918a-c0abe5b1473b | 
| timestamp | A timestamp in milliseconds for the request&nbsp;&lt;br&gt; | 1540457718692 | 
{% /table %}

This API request must also use the authorisation headers describe above.

Upon a successful upload of the requested resource media, the user will be redirected to a relying party defined success page. This can occur in a number of different configurations:

1. If the success URL is defined in the create session request, the user will be redirected here.
2. If no success URL has been defined and the relying part is using the Iframe configuration Yoti will send a success POST request back to the site, the business can then decide how to respond within the user journey.

Upon an unsuccessful capture of the requested resource media, caused by an error or a failure after 3 submission attempts. The Yoti Client SDK will redirect to the Error URL (If defined in the create session request). In the call to this Error URL, additional information will be provided through an error code that is provided as a query string parameter.

## State retrieval

Yoti will provide back a state of the transaction.

{% table %}
| State | Description | 
| ---- | ---- | 
| ONGOING | Yoti is still working on tasks and checks for the users ID. | 
| COMPLETED | Yoti has completed checks and tasks. | 
| EXPIRED | Yoti could not complete the checks and tasks. | 
{% /table %}

{% code %}
{% tab language="json" %}
{
  "client_session_token_ttl" : 599,
  "session_id" : "<uuid>",
  "user_tracking_id" : "<uuid>",
  "state" : "ONGOING",
  "client_session_token" : "<uuid>",
}
{% /tab %}
{% /code %}

## Resources retrieval

The resources retrieval returns back values of the document type.

{% table %}
| Response Topic | Response | Description | 
| ---- | ---- | ---- | 
| ID Document | PASSPORT,&lt;br&gt;DRIVING LICENSE, &lt;br&gt;NATIONAL ID | ID document types the user has sent through. | 
| Issuing Country | e.g. GBR | A&nbsp; ISO 3 letter country code | 
| Capture method | CAMERA,&lt;br&gt;UPLOAD&nbsp; | If a picture of the ID was taken by the user or uploaded. | 
{% /table %}

The liveness check will produce 3 image media resources taken from the camera and it will also produce a binary facemap of the user.

{% code %}
{% tab language="json" %}
"resources" : {
    "id_documents" : [
      {
        "id" : "<uuid>",
        "document_type" : "PASSPORT"
        "issuing_country" : "GBR",
        "pages" : [
          {
            "capture_method" : "CAMERA"
            "media" : {
              "id" : "<uuid>",
              "type" : "IMAGE",
              "created" : "<yyyy-mm-ddThh:mm:ssZ>",
              "last_updated" : "<yyyy-mm-ddThh:mm:ssZ>"
            },
          }
        ],
"liveness_capture": [
            {
                "id": "<uuid>",
                "tasks": [],
                "frames": [
                    {
                        "media": {
                            "id": "<uuid>",
                            "type": "IMAGE",
                            "created": "<yyyy-mm-ddThh:mm:ssZ>",
                            "last_updated": "<yyyy-mm-ddThh:mm:ssZ>"
                        }
                    },
                    {
                        "media": {
                            "id": "<uuid>",
                            "type": "IMAGE",
                            "created": "<yyyy-mm-ddThh:mm:ssZ>",
                            "last_updated": "<yyyy-mm-ddThh:mm:ssZ>"
                        }
                    },
                    {
                        "media": {
                            "id": "<uuid>",
                            "type": "IMAGE",
                            "created": "<yyyy-mm-ddThh:mm:ssZ>",
                            "last_updated": "<yyyy-mm-ddThh:mm:ssZ>"
                        }
                    },
                    {},
                    {},
                    {},
                    {}
                ],
                "liveness_type": "ZOOM",
                "facemap": {
                    "media": {
                        "id": "<uuid>",
                        "type": "BINARY",
                        "created": "<yyyy-mm-ddThh:mm:ssZ>",
                        "last_updated": "<yyyy-mm-ddThh:mm:ssZ>"
                    }
                }
            }
]
{% /tab %}
{% /code %}

## Document fields retrieval

This is where all the users details will be post verification and what format. See document fields section below for an example.

{% code %}
{% tab language="json" %}
"document_fields" : {
          "media" : {
            "id" : "<uuid>",
            "type" : "JSON",
            "created" : "<yyyy-mm-ddThh:mm:ssZ>",
            "last_updated" : "<yyyy-mm-ddThh:mm:ssZ>"
          }
{% /tab %}
{% /code %}

## Tasks retrieval

Status of the data extraction task from Yoti.

{% table %}
| State | Description | 
| ---- | ---- | 
| DONE | The task is completed | 
| PENDING | The task is being completed | 
| FAILED | The task could not be completed | 
{% /table %}

{% code %}
{% tab language="json" %}
"tasks" : [
          {
            "id" : "<uuid>",
            "type" : "ID_DOCUMENT_TEXT_DATA_EXTRACTION",
            "state" : "DONE", // | "PENDING" | "FAILED"
            "created" : "<yyyy-mm-ddThh:mm:ssZ>",
            "last_updated" : "<yyyy-mm-ddThh:mm:ssZ>",
            "generated_media" : [
              {
                "id" : "<uuid>",
                "type" : "JSON"
              }
            ],
{% /tab %}
{% /code %}

## Checks retrieval

We provide back the following details for the checks:

### ID_DOCUMENT_AUTHENTICITY

{% table %}
| Response Topic | Response | Description | 
| ---- | ---- | ---- | 
| Status | CREATED, &lt;br&gt;PENDING,&lt;br&gt;INTERNAL ERROR | &lt;p&gt;The status of the verification from Yoti after performing the follow checks:&lt;br&gt;-no_sign_of_tampering&lt;br&gt;-real_document&lt;br&gt;-data_in_correct_position&lt;br&gt;-expected_data_present&lt;br&gt;-document_in_date&lt;br&gt;-other_security_features&lt;/p&gt; | 
| Recommendation | APPROVE,&lt;br&gt;REJECT,&lt;br&gt;NOT AVAILABLE | Yoti will provide you a recommendation based on the checks. You can tailor this as you see fit. | 
{% /table %}

**Example of an approved report**

{% code %}
{% tab language="json" %}
"checks": [
      {
         "type": "ID_DOCUMENT_AUTHENTICITY",
         "id": "<uuid>",
         "state": "DONE",
         "resources_used": [
            "<uuid>"
         ],
         "generated_media": [],
         "report": {
            "recommendation": {
               "value": "APPROVE"
            },
            "breakdown": [
               {
                  "sub_check": "no_sign_of_tampering",
                  "result": "PASS",
                  "details": []
               },
               {
                  "sub_check": "real_document",
                  "result": "PASS",
                  "details": []
               },
               {
                  "sub_check": "data_in_correct_position",
                  "result": "PASS",
                  "details": []
               },
               {
                  "sub_check": "expected_data_present",
                  "result": "PASS",
                  "details": []
               },
               {
                  "sub_check": "other_security_features",
                  "result": "PASS",
                  "details": []
               },
               {
                  "sub_check": "document_in_date",
                  "result": "PASS",
                  "details": []
               }
            ]
         },
         "created": "<yyyy-mm-ddThh:mm:ssZ>",
         "last_updated": "<yyyy-mm-ddThh:mm:ssZ>"
      }
]
{% /tab %}
{% /code %}

If Yoti responds with the REJECT recommendation it will be for the following reason:

- Missing Hologram
- Document Copy
- Tampered

**Example of a rejected report**

{% code %}
{% tab language="json" %}
"checks": [
   {
      "id" : "<uuid>",
      "type" : "ID_DOCUMENT_AUTHENTICITY",
      "state" : "DONE", 
      "resources_used" : ["<uuid>"],
      "report" : {
        "recommendation": {
          "value" : "REJECT",
          "reason" : "NOT_GENUINE" 
        },
        "breakdown": [
               {
                  "sub_check": "no_sign_of_tampering",
                  "result": "PASS",
                  "details": []
               },
               {
                  "sub_check": "real_document",
                  "result": "PASS",
                  "details": []
               },
               {
                  "sub_check": "data_in_correct_position",
                  "result": "FAIL",
                  "details": []
               },
               {
                  "sub_check": "expected_data_present",
                  "result": "PASS",
                  "details": []
               },
               {
                  "sub_check": "other_security_features",
                  "result": "FAIL",
                  "details": []
               },
               {
                  "sub_check": "document_in_date",
                  "result": "FAIL",
                  "details": []
               }
        ]
      },
      "created" : "<yyyy-mm-ddThh:mm:ssZ>",
      "last_updated" : "<yyyy-mm-ddThh:mm:ssZ>"
    }
  ]
{% /tab %}
{% /code %}

If Yoti responds with the NOT AVAILABLE recommendation, this means that a requested check was not sufficient to complete the check. A full list of  possible reasons can be found below:

{% table %}
| Yoti Response | Description | 
| ---- | ---- | 
| DOCUMENT&lt;i&gt;_&lt;/i&gt;NOT_SUPPORTED | Document not supported&lt;br&gt; | 
| DOCUMENT_VERSION_NOT_SUPPORTED | Template not Yoti data sources&lt;br&gt; | 
| NON_LATIN&lt;i&gt;_&lt;/i&gt;ALPHABET | Non-latin alphabet | 
| IMAGE_CORRUPTED | Image(s) corrupted/no image openable | 
| PHOTO_TOO_BLURRY | Photo too blurry | 
| PHOTO_TOO_DARK | Too dark | 
| PHOTO_OVEREXPOSED | Too light (overexposed) | 
| PARTIAL_PHOTO | Partial photo | 
| OBJECT_OBSTRUCTION | Object in the way | 
| GLARE_OBSTRUCTION | Reflection / hologram in the way (to the point we can’t do the check) | 
| DOCUMENT_TOO_DAMAGED | Document damaged (to the point we can’t do the check) | 
| MISSING_DOCUMENT_SIDE | Missing Document side | 
| IMAGE_RESOLUTION_TOO_LOW | Insufficient image resolution | 
| UNABLE_TO_LOAD | Unable to load file | 
| BLACK_AND&nbsp;WHITE_IMAGE | Black and white image | 
{% /table %}

**Example of a NOT AVAILABLE report**

{% code %}
{% tab language="json" %}
"checks": [
 {
      "type" : "ID_DOCUMENT_AUTHENTICITY",
      "id" : "<uuid>",
      "state" : "DONE"
      "resources_used" : ["<uuid>"],
      "report" : {
        "recommendation": {
          "value" : "NOT_AVAILABLE",
          "reason" : "PICTURE_TOO_DARK"
          "recovery_suggestion" : "BETTER_LIGHTING" 
        },
        "breakdown": [
          {
            "sub_check": "issuing_authority_verification",
            "result": "PASS"
          }
        ]
      },
      "created" : "<yyyy-mm-ddThh:mm:ssZ>",
      "last_updated" : "<yyyy-mm-ddThh:mm:ssZ>"
    }
]
{% /tab %}
{% /code %}

### LIVENESS

Liveness checks can be retried if failed, depending on specified limited set when generating the session. Each try will generate a new report in the JSON response. The check will either be approved or rejected based on the result of the liveness from ZoOm which is a pass/fail result.

**Example of a liveness report**

{% code %}
{% tab language="json" %}
"checks": [
  {
         "type": "LIVENESS",
         "id": "<uuid>",
         "state": "DONE",
         "resources_used": [
            "<uuid>"
         ],
         "generated_media": [],
         "report": {
            "recommendation": {
               "value": "APPROVE" //"REJECT"
            },
            "breakdown": [
               {
                  "sub_check": "liveness_auth",
                  "result": "PASS", //"FAIL"
                  "details": []
               }
            ]
         },
         "created": "<yyyy-mm-ddThh:mm:ssZ>",
         "last_updated": "<yyyy-mm-ddThh:mm:ssZ>"
      }
]
{% /tab %}
{% /code %}

### ID_DOCUMENT_FACE_MATCH

A ID_DOCUMENT_FACE_MATCH check will return a report containing the sub checks, manual check or machine check.

A manual check will be either a pass or a fail. The machine check will be a pass or fail and will have further details, which will be a confidence score out of 1. The face match check will give a recommendation based on these as either APPROVE or REJECT.

**Example of a face match report**

{% code %}
{% tab language="json" %}
{
            "type": "ID_DOCUMENT_FACE_MATCH",
            "id": "<uuid>",
            "state": "DONE",
            "resources_used": [
                "<uuid>",
                "<uuid>"
            ],
            "generated_media": [],
            "report": {
                "recommendation": {
                    "value": "APPROVE" // "REJECT"
                },
                "breakdown": [
                    {
                        "sub_check": "manual_face_match",
                        "result": "PASS", // "FAIL"
                        "details": []
                    },
                    {
                        "sub_check": "ai_face_match",
                        "result": "PASS", // "FAIL"
                        "details": [
                            {
                                "name": "confidence_score",
                                "value": "1.00"
                            }
                        ]
                    }
                ]
            },
            "created": "<yyyy-mm-ddThh:mm:ssZ>",
            "last_updated": "<yyyy-mm-ddThh:mm:ssZ>"
        }
{% /tab %}
{% /code %}

### Example of full payload response

{% code %}
{% tab language="json" %}
{
  "client_session_token_ttl" : 599,
  "session_id" : "<uuid>",
  "user_tracking_id" : "<uuid>",
  "state" : "ONGOING",
  "client_session_token" : "<uuid>",
  "resources" : {
    "id_documents" : [
      {
        "id" : "<uuid>",
        "document_type" : "PASSPORT"
        "issuing_country" : "GBR",
        "pages" : [
          {
            "capture_method" : "CAMERA"
            "media" : {
              "id" : "<uuid>",
              "type" : "IMAGE",
              "created" : "<yyyy-mm-ddThh:mm:ssZ>",
              "last_updated" : "<yyyy-mm-ddThh:mm:ssZ>"
            },
          }
        ],
        "document_fields" : {
          "media" : {
            "id" : "<uuid>",
            "type" : "JSON",
            "created" : "<yyyy-mm-ddThh:mm:ssZ>",
            "last_updated" : "<yyyy-mm-ddThh:mm:ssZ>"
          }
        },
        "tasks" : [
          {
            "id" : "<uuid>",
            "type" : "ID_DOCUMENT_TEXT_DATA_EXTRACTION",
            "state" : "DONE", // | "PENDING" | "FAILED"
            "created" : "<yyyy-mm-ddThh:mm:ssZ>",
            "last_updated" : "<yyyy-mm-ddThh:mm:ssZ>",
            "generated_media" : [
              {
                "id" : "<uuid>",
                "type" : "JSON"
              }
            ],
            "generated_checks" : [
              {
                "id" : "<uuid>",
                "type" : "ID_DOCUMENT_TEXT_DATA_CHECK"
              }
            ]
          }
        ]
      }
    ],
  },
  "checks" : [
    {
      "id" : "<uuid>",
      "type" : "ID_DOCUMENT_AUTHENTICITY", 
      "state" : "DONE"
      "resources_used" : ["<uuid>"],
      "report" : {
        "recommendation": {
          "value" : "APPROVE"
        },
        "breakdown": [
             {
                  "sub_check": "no_sign_of_tampering",
                  "result": "PASS",
                  "details": []
               },
               {
                  "sub_check": "real_document",
                  "result": "PASS",
                 "details": []

               },
               {
                  "sub_check": "data_in_correct_position",
                  "result": "PASS",
                  "details": []
               },
               {
                  "sub_check": "expected_data_present",
                  "result": "PASS",
                  "details": []
               },
               {
                  "sub_check": "other_security_features",
                  "result": "PASS",
                  "details": []
               },
               {
                  "sub_check": "document_in_date",
                  "result": "PASS",
                  "details": []
               }
        ]
      },
      "created" : "<yyyy-mm-ddThh:mm:ssZ>",
      "last_updated" : "<yyyy-mm-ddThh:mm:ssZ>"
    }
  ]
}
{% /tab %}
{% /code %}

### Other response codes

{% table %}
| Code | Descriptions | 
| ---- | ---- | 
| 200 | OK | 
| 400 | Bad Request | 
| 401 | Unauthorised request. Wrong key or signature. | 
| 404 | Session not found | 
{% /table %}

### Document fields explained

This is the JSON version of the user.

{% code %}
{% tab language="json" %}
{
  // FullName contains given names and family name.
  "full_name" : "Jon Jim Foo",
  // DateOfBirth is the date of birth in the form yyyy-mm-dd.
  "date_of_birth" : "2000-12-01",
  // Nationality is the nationality expressed as
  // an ISO/ICAO alpha-3 country code.
  "nationality" : "GBR",
  // GivenNames contains first and middle names.
  "given_names" : "Jon Jim",
  // FirstName is the first name only.
  "first_name" : "Jon",
  // MiddleName is the middle name only.
  "middle_name" : "Jim",
  // FamilyName is the family name.
  "family_name" : "Foo",
  // PlaceOfBirth is the place of birth,
  // it may contain a country name or a city name or both.
  "place_of_birth" : "London",
  // CountryOfBirth is the country of birth,
  // as an ISO/ICAO alpha-3 country code.
  "country_of_birth" : "GBR",
  // Gender is the gender and can be any of the
  // following values:
  // "MALE", "FEMALE", "TRANSGENDER" or "OTHER".
  "gender" : "MALE",
  // NamePrefix is the name prefix, for example a title.
  "name_prefix" : "Dr",
  // NameSuffix is the name suffix.
  "name_suffix" : "Jr",
  // FirstNameAlias is the alias for the first name.
  "first_name_alias" : "",
  // MiddleNameAlias is the alias for the middle name.
  "middle_name_alias" : "",
  // FamilyNameAlias is the alias for the family name.
  "family_name_alias" : "",
  // Weight is the weight as displayed on the document.
  // Should contain weight and the unit.
  "weight" : "",
  // Height is the height as displayed on the document.
  // Should contain height and the unit.
  "height" : "",
  // EyeColor is the eye colour as displayed on the document.
  "eye_color" : "",
  "structured_postal_address" : {},
  // DocumentType specifies the type of document.
  // Values: "DRIVING_LICENCE", "PASSPORT", "NATIONA_ID"
  "document_type" : "DRIVING_LICENCE",
  // IssuingCountry is the country the document was issued in.
  // Defined as an ISO/ICAO alpha-3 country code.
  "issuing_country" : "GBR",
  // DocumentNumber is the document number.
  "document_number" : "EF1523467",
  // ExpirationDate defines the date of expire for the document
  // in the form yyyy-mm-dd.
  "expiration_date" : "2030-12-01",
  // DateOfIssue is the date of issue of the document
  // in the form yyyy-mm-dd.
  "date_of_issue" : "2001-12-01",
  // IssuingAuthority is the authority that issued the document.
  "issuing_authority" : "DVLA",
  // MRZ provides the content of the machine readable zone,
  // as displayed on the document.
  "mrz" : {/*see MRZ object*/}
}
{% /tab %}
{% /code %}

### Address

The address format is in the following [section](/yoti-app/yoti-attributes-explained#address-attributes). 

---

### MRZ

This is the JSON version of the user.

{% code %}
{% tab language="json" %}
{  
  "type" : 1, // 1=TD1, 2=TD3,
  "line1" : "<<<<<...",
  "line2" : "<<<<<...",
  "line3" : "<<<<<..."
}
{% /tab %}
{% /code %}