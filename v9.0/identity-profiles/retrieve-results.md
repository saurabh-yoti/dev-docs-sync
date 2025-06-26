---
type: page
title: Retrieve results
listed: true
slug: retrieve-results
description: 
index_title: Retrieve results
hidden: 
keywords: 
tags: 
---

Each session has a configured 'time to live' (TTL) which must be above 300 seconds (5 minutes). When a session is created, it remains active until its 'time to live' is reached.
For any active session, you can use the Yoti SDK to retrieve a report on the session (containing the end-user's uploaded documents and associated metadata).

{% html %}
<div class="alert-know">
    <div class="alert-title" id="know">
        Recommendation
    </div>
    <div class="alert-text">
Yoti strongly recommends you use notifications for each session status.    </div>
    <div class="alert-links"> 
       <a href="https://developers.yoti.com/identity-profiles/notifications">Notifications</a>
    </div>
</div>
{% /html %}

This page explains how to:

- Retrieve the results of the session.
- Retrieve the associated media.
- Display the Identity Profile Report for the session.

---

## Result of the session

Session retrieval requires a session ID, this is generated from the create a session endpoint.  Below is a basic example of what retrieving a session looks like:

{% code %}
{% tab language="javascript" %}
// Returns a session result
const sessionResult = await idvClient.getSession(sessionId);

// Returns the session state
const state = sessionResult.getState();

// Returns session resources
const resources = session.getResources();
{% /tab %}
{% tab language="java" %}
// Returns a session result
GetSessionResult sessionResult = docScanClient.getSession(sessionId);

// Returns the session state
String state = sessionResult.getState();

// Returns session resources
ResourceContainer resources = sessionResult.getResources();
{% /tab %}
{% tab language="php" %}
// Returns a session result
$sessionResult = $docScanClient->getSession($sessionId);

// Returns the session state
$state = $sessionResult->getState();

// Returns session resources
$resources = $sessionResult->getResources();
{% /tab %}
{% tab language="csharp" %}
// Returns a session result
GetSessionResult sessionResult = docScanClient.GetSession(sessionId);

// Returns the session state
string state = sessionResult.State;

// Returns session resources
ResourceContainer resources = sessionResult.Resources;
{% /tab %}
{% tab language="go" %}
// Returns a session result
sessionResult, err := client.GetSession(sessionId)
if err != nil {
  	return nil, err
}

// Returns the session state
state = sessionResult.State

// Returns session resources
resources = sessionResult.Resources
{% /tab %}
{% /code %}

The following are present in every session result:

{% table %}
| Value | Description | 
| ---- | ---- | 
| State | The current state of the session. It provides the overall state of the session. \n\n\n\nYou can search through session results prior to this being completed, but some checks may not have been processed yet. | 
| Resources | A container of all ID documents and liveness captures for this session. | 
| Checks | A container of all checks performed for this session. | 
{% /table %}

---

## Retrieve the Media

Document images from the user, text extraction fields and liveness captures for the session are available inside the resources container. These can be retrieved by looking at the relevant media ID inside the documents collection.

{% code %}
{% tab language="javascript" %}
// Returns a collection of ID Documents
const idDocuments = resources.getIdDocuments();

// Returns document fields object
const documentFields = idDocuments[0].getDocumentFields();

const mediaId = documentFields.getMedia().getId();
const media = await idvClient.getMediaContent(sessionId, mediaId);

const buffer = media.getContent();
const base64Content = media.getBase64Content();
const mimeType = media.getMimeType();
{% /tab %}
{% tab language="java" %}
// Returns a collection of ID Documents
List<? extends IdDocumentResourceResponse> idDocuments = resources.getIdDocuments();

String mediaId = idDocuments[0].getDocumentFields()..getMedia().getId();

Media media = docScanClient.getMediaContent(sessionId, mediaId);
{% /tab %}
{% tab language="php" %}
// Returns a collection of ID Documents
$idDocuments = $resources->getIdDocuments();

$mediaId = $idDocuments[0]->getDocumentFields()->getMedia()->getId();

$media = $docScanClient->getMediaContent($sessionId, $mediaId);
$base64Content = $media->getBase64Content();
$contentType = $media->getMimeType();
{% /tab %}
{% tab language="csharp" %}
// Returns a collection of ID Documents
List<IdDocumentResourceResponse> idDocuments = resources.IdDocuments;

string mediaId = idDocuments[0].DocumentFields.Media.Id();

MediaValue media = docScanClient.GetMediaContent(sessionId, mediaId);
{% /tab %}
{% tab language="go" %}
// Returns a collection of ID Documents
idDocuments = resources.IDDocuments

// Returns document fields object
documentFields = idDocuments[0].DocumentFields
mediaID = documentFields.Media.ID

media, err := client.GetMediaContent(sessionId, mediaID)
if err != nil {
  	return nil, err
}

mimeType = media.MIME()
data = media.Data()
{% /tab %}
{% /code %}

---

## Retrieve the Identity Profile

Once the session has reached the state of 'Completed', identity profile can be successfully retrieved.

In case of a successful transaction, once the identity profile is received, the identity profile report JSON will be accessible. This contains the media ID which can then be used to get the full JSON response of the report.

{% code %}
{% tab language="javascript" %}
const identityProfile = sessionResult.getIdentityProfile();
const identityProfileReport = identityProfile.getIdentityProfileReport();

const mediaId = identityProfileReport.getMedia().getId();
const identityProfileReportMedia = await idvClient.getMediaContent(sessionId, mediaId);

const identityProfileReportMediaBuffer = identityProfileReportMedia.getContent();
{% /tab %}
{% tab language="java" %}
IdentityProfile identityProfile = sessionResult.getIdentityProfile();
IdentityProfileReport identityProfileReport = identityProfile.getIdentityProfileReport();

String mediaID = identityProfileReport.getMedia().getId();
Media identityProfileReportMedia = await docScanClient.getMediaContent(sessionId, mediaId);
{% /tab %}
{% tab language="php" %}
$identityProfile = $sessionResult->getIdentityProfile();
$identityProfileReport = $identityProfile->getIdentityProfileReport();

$mediaID = identityProfileReport->getMedia()->getId();

$identityProfileReportMedia = $docScanClient->getMediaContent($sessionId, $mediaId);
$base64Content = $media->getBase64Content();
$contentType = $media->getMimeType();
{% /tab %}
{% tab language="csharp" %}
string mediaId = sessionResult.IdentityProfile.Report["media"]["id"].ToString();
MediaValue mediaValue = docScanClient.GetMediaContent(sessionId, mediaId);

byte[] identityProfileReport = mediaValue.GetContent();
{% /tab %}
{% tab language="go" %}
identityProfile = sessionResult.IdentityProfileResponse
identityProfileReport = identityProfile.IdentityProfileResponse.Report

media, err := identityProfile.Report["media"].(map[string]interface{})
mediaID, err := media["id"].(string)

identityProfileReportMedia, err := client.GetMediaContent(sessionId, mediaID)
{% /tab %}
{% /code %}

{% html %}
<div class="alert-GTK">
    <div class="alert-title" id="GTK">
        Jump to..
    </div>
    <div class="alert-text">
        Get a deeper dive on the identity profile and understanding the report.
    </div>
    <div class="alert-links"> 
        <a href="https://developers.yoti.com/identity-profilesidentity-profile-report">Identity Profile Report</a>        
   </div>
</div>
{% /html %}

---

## Session Result Parameters

The session result contains the session metadata, ID checks, uploaded documents and the identity profile report.

{% table %}
| Parameter | Type | Description | Included | 
| ---- | ---- | ---- | ---- | 
| SessionResult | Object | Complete Session Result | Always | 
| sessionId | String | Unique Session ID | Always | 
| userTrackingId | String | Unique User Tracking ID | Optional | 
| state | String | The current state of the session. \n\n\n\nEnum: ONGOING, COMPLETED, EXPIRED | Always | 
| clientSessionToken | String | Token for the user session. | Optional | 
| clientSessionTokenTtl | Integer | Remaining time the user has to complete the session. | Optional | 
| checks | []Object | List of all the checks performed. | Always | 
| resources | Object | Collection of all the resources created. | Always | 
| biometricConsent | String | Collected biometric consent. | Conditional | 
| identityProfile | Object | Complete Identity profile\n\n\n\n(Available when the session is completed). | Always | 
| subjectId | String | Subject identifier provided by the RP at session creation time. | Optional | 
| result | String | Final result of the identity verification. \n\n\n\n'Done' means the identity could be verified and the identity profile report provided. 'Aborted' means the user could not be verified and no identity profile report produced, all the resources and checks are still available. \n\n\n\nEnum: DONE, ABORTED | Always | 
| failureReason | Object | In case of _result: ABORTED,_ reason for the failure. | Optional | 
| reasonCode | String | Reason code for the failure. Please see error codes for full list | Conditional | 
| identityProfileReport | Object | The identity profile report media contains the identity attributes and the verification report that certifies the scheme compliance and achieved verification level. | Conditional | 
| trustFramework | String | Defines under which trust framework this identity was verified. As defined at session creation time. \n\n\n\nEnum: UK_TFIDA, YOTI_GLOBAL | Conditional | 
| schemesCompliance | []Object | Defines which schemes (of the requested ones) this identity profile satisfies. | Conditional | 
| scheme | Boolean | Scheme defines the identity scheme. | Conditional | 
| requirementsMet | String | Asserts whether the identity scheme requirements were met or not. | Conditional | 
| requirementsNotMetInfo | Object | Provides info on why the scheme requirements were not met. | Conditional | 
| media | String | Full identity profile report provided as a JSON media. | Conditional | 
| created | String | Uses the ISO8601 standard representation of date times. | Conditional | 
| last_updated | String | Uses the ISO8601 standard representation of date times. | Conditional | 
| id | String | Identifier to be used to fetch this media. | Conditional | 
| type | String | JSON Enum: IMAGE, JSON,BINARY | Conditional | 
{% /table %}

---

## Example JSON Response

{% code %}
{% tab language="json" %}
{
    "client_session_token_ttl": 8490,
    "session_id": "52098976-42d0-4051-a80f-7fc3438e4d9e",
    "state": "COMPLETED",
    "resources": {
        "id_documents": [
            {
                "id": "9fc63ad4-755d-46d7-a8c4-289e8296d0ce",
                "tasks": [
                    {
                        "type": "ID_DOCUMENT_TEXT_DATA_EXTRACTION",
                        "id": "9d4a3aeb-949d-47fe-b6f4-da68dd7993af",
                        "state": "DONE",
                        "created": "2024-06-24T14:43:40Z",
                        "last_updated": "2024-06-24T14:44:09Z",
                        "generated_checks": [],
                        "generated_media": [
                            {
                                "id": "cca362fc-fc05-4221-87a1-8c33ec0aec90",
                                "type": "JSON"
                            }
                        ],
                        "recommendation": {
                            "value": "PROGRESS"
                        }
                    }
                ],
                "source": {
                    "type": "END_USER"
                },
                "created_at": "2024-06-24T14:43:40Z",
                "last_updated": "2024-06-24T14:44:09Z",
                "document_type": "PASSPORT",
                "issuing_country": "GBR",
                "pages": [
                    {
                        "capture_method": "CAMERA",
                        "media": {
                            "id": "e18a77b5-f45e-47e1-92d5-c0d4a34a6383",
                            "type": "IMAGE",
                            "created": "2024-06-24T14:43:59Z",
                            "last_updated": "2024-06-24T14:43:59Z"
                        },
                        "frames": [
                            {
                                "media": {
                                    "id": "0cb9158b-7940-49af-a72c-bf2f9711c154",
                                    "type": "IMAGE",
                                    "created": "2024-06-24T14:44:04Z",
                                    "last_updated": "2024-06-24T14:44:04Z"
                                }
                            },
                            {
                                "media": {
                                    "id": "a26448a3-2849-4147-8cde-2580727361be",
                                    "type": "IMAGE",
                                    "created": "2024-06-24T14:44:04Z",
                                    "last_updated": "2024-06-24T14:44:04Z"
                                }
                            },
                            {
                                "media": {
                                    "id": "bbd86a22-e909-42a7-bb8c-ce2f8db83921",
                                    "type": "IMAGE",
                                    "created": "2024-06-24T14:44:05Z",
                                    "last_updated": "2024-06-24T14:44:05Z"
                                }
                            }
                        ]
                    }
                ],
                "document_fields": {
                    "media": {
                        "id": "cca362fc-fc05-4221-87a1-8c33ec0aec90",
                        "type": "JSON",
                        "created": "2024-06-24T14:44:09Z",
                        "last_updated": "2024-06-24T14:44:09Z"
                    }
                },
                "document_id_photo": {
                    "media": {
                        "id": "323eda4e-c32a-4d4b-9ee9-1fbfe9701000",
                        "type": "IMAGE",
                        "created": "2024-06-24T14:44:09Z",
                        "last_updated": "2024-06-24T14:44:09Z"
                    }
                }
            }
        ],
        "supplementary_documents": [],
        "liveness_capture": [
            {
                "id": "ef068fbc-71d2-4fcf-8db3-0260dcd510c7",
                "tasks": [],
                "source": {
                    "type": "END_USER"
                },
                "created_at": "2024-06-24T14:45:05Z",
                "last_updated": "2024-06-24T14:45:29Z",
                "frames": [
                    {
                        "media": {
                            "id": "77460817-723d-464b-a78f-eb3980002e3f",
                            "type": "IMAGE",
                            "created": "2024-06-24T14:45:26Z",
                            "last_updated": "2024-06-24T14:45:26Z"
                        }
                    },
                    {
                        "media": {
                            "id": "8bbc343a-7632-4e18-9f03-1fc84470877b",
                            "type": "IMAGE",
                            "created": "2024-06-24T14:45:26Z",
                            "last_updated": "2024-06-24T14:45:26Z"
                        }
                    },
                    {
                        "media": {
                            "id": "24bafb64-464f-4e10-981b-9b8c52d4e6a3",
                            "type": "IMAGE",
                            "created": "2024-06-24T14:45:25Z",
                            "last_updated": "2024-06-24T14:45:25Z"
                        }
                    },
                    {
                        
                    },
                    {
                        
                    },
                    {
                        
                    },
                    {
                        
                    }
                ],
                "liveness_type": "ZOOM",
                "facemap": {
                    "media": {
                        "id": "1df30c53-b2a2-49b9-9265-5015f86cbcb3",
                        "type": "BINARY",
                        "created": "2024-06-24T14:45:29Z",
                        "last_updated": "2024-06-24T14:45:29Z"
                    }
                }
            }
        ],
        "face_capture": [],
        "applicant_profiles": [
            {
                "id": "5b8b561c-b974-4c1b-addf-bfa1e7d9b19f",
                "tasks": [],
                "source": {
                    "type": "END_USER"
                },
                "created_at": "2024-06-24T14:44:11Z",
                "last_updated": "2024-06-24T14:44:14Z",
                "media": {
                    "id": "c0114acc-e8d3-4c93-99ac-6058e09798c2",
                    "type": "JSON",
                    "created": "2024-06-24T14:44:14Z",
                    "last_updated": "2024-06-24T14:44:14Z"
                }
            }
        ]
    },
    "checks": [
        {
            "type": "ID_DOCUMENT_AUTHENTICITY",
            "id": "d4af854f-a0af-4fe3-8ae7-03dc6a99b802",
            "state": "DONE",
            "resources_used": [
                "9fc63ad4-755d-46d7-a8c4-289e8296d0ce",
                "ef068fbc-71d2-4fcf-8db3-0260dcd510c7"
            ],
            "generated_media": [],
            "report": {
                "recommendation": {
                    "value": "APPROVE"
                },
                "breakdown": [
                    {
                        "sub_check": "age_estimation_dob_comparison",
                        "result": "PASS",
                        "details": [],
                        "process": "AUTOMATED"
                    },
                    {
                        "sub_check": "document_in_date",
                        "result": "PASS",
                        "details": [],
                        "process": "AUTOMATED"
                    },
                    {
                        "sub_check": "document_recognition",
                        "result": "PASS",
                        "details": [],
                        "process": "AUTOMATED"
                    },
                    {
                        "sub_check": "fraud_list_check",
                        "result": "PASS",
                        "details": [],
                        "process": "AUTOMATED"
                    },
                    {
                        "sub_check": "hologram",
                        "result": "PASS",
                        "details": [],
                        "process": "EXPERT_REVIEW"
                    },
                    {
                        "sub_check": "hologram_movement",
                        "result": "FAIL",
                        "details": [],
                        "process": "EXPERT_REVIEW"
                    },
                    {
                        "sub_check": "mrz_validation",
                        "result": "PASS",
                        "details": [],
                        "process": "AUTOMATED"
                    },
                    {
                        "sub_check": "no_sign_of_forgery",
                        "result": "PASS",
                        "details": [],
                        "process": "EXPERT_REVIEW"
                    },
                    {
                        "sub_check": "no_sign_of_tampering",
                        "result": "PASS",
                        "details": [],
                        "process": "EXPERT_REVIEW"
                    },
                    {
                        "sub_check": "ocr_mrz_comparison",
                        "result": "FAIL",
                        "details": [
                            {
                                "name": "date_of_birth",
                                "value": "MATCH"
                            },
                            {
                                "name": "document_number",
                                "value": "MISMATCH"
                            },
                            {
                                "name": "expiration_date",
                                "value": "MATCH"
                            },
                            {
                                "name": "gender",
                                "value": "MATCH"
                            },
                            {
                                "name": "name",
                                "value": "MISMATCH"
                            }
                        ],
                        "process": "AUTOMATED"
                    },
                    {
                        "sub_check": "other_security_features",
                        "result": "PASS",
                        "details": [],
                        "process": "EXPERT_REVIEW"
                    },
                    {
                        "sub_check": "physical_document_captured",
                        "result": "PASS",
                        "details": [],
                        "process": "EXPERT_REVIEW"
                    },
                    {
                        "sub_check": "portrait_integrity",
                        "result": "PASS",
                        "details": [
                            {
                                "name": "portrait_substitution_trust_score",
                                "value": "0.99"
                            },
                            {
                                "name": "portrait_substitution",
                                "value": "VERY_UNLIKELY"
                            }
                        ],
                        "process": "AUTOMATED"
                    },
                    {
                        "sub_check": "yoti_fraud_list_check",
                        "result": "PASS",
                        "details": [
                            {
                                "name": "provider_org",
                                "value": "Yoti Ltd"
                            }
                        ],
                        "process": "AUTOMATED"
                    }
                ]
            },
            "created": "2024-06-24T14:45:32Z",
            "last_updated": "2024-06-24T14:46:57Z"
        },
        {
            "type": "LIVENESS",
            "id": "0f49977b-4798-4bb0-9511-c0d0db75e98e",
            "state": "DONE",
            "resources_used": [
                "ef068fbc-71d2-4fcf-8db3-0260dcd510c7"
            ],
            "generated_media": [],
            "report": {
                "recommendation": {
                    "value": "APPROVE"
                },
                "breakdown": [
                    {
                        "sub_check": "liveness_auth",
                        "result": "PASS",
                        "details": [],
                        "process": "AUTOMATED"
                    }
                ]
            },
            "created": "2024-06-24T14:45:29Z",
            "last_updated": "2024-06-24T14:45:31Z"
        },
        {
            "type": "ID_DOCUMENT_FACE_MATCH",
            "id": "f314aa90-fcb4-4028-aac4-51b98069e796",
            "state": "DONE",
            "resources_used": [
                "9fc63ad4-755d-46d7-a8c4-289e8296d0ce",
                "ef068fbc-71d2-4fcf-8db3-0260dcd510c7"
            ],
            "generated_media": [],
            "report": {
                "recommendation": {
                    "value": "APPROVE"
                },
                "breakdown": [
                    {
                        "sub_check": "ai_face_match",
                        "result": "PASS",
                        "details": [
                            {
                                "name": "confidence_score",
                                "value": "0.68"
                            }
                        ],
                        "process": "AUTOMATED"
                    }
                ]
            },
            "created": "2024-06-24T14:45:32Z",
            "last_updated": "2024-06-24T14:45:35Z"
        }
    ],
    "biometric_consent": "2024-06-24T14:44:33Z",
    "advanced_identity_profile": {
        "result": "DONE",
        "identity_profile_report": {
            "compliance": [
                {
                    "trust_framework": "YOTI_GLOBAL",
                    "schemes_compliance": [
                        {
                            "scheme": {
                                "type": "IDENTITY",
                                "objective": "AL_M1",
                                "label": "EXAMPLEALL1"
                            },
                            "requirements_met": true
                        }
                    ]
                }
            ],
            "media": {
                "id": "86358d21-5943-4e80-864a-c78b3a24c275",
                "type": "JSON",
                "created": "2024-06-24T14:46:58Z",
                "last_updated": "2024-06-24T14:46:58Z"
            }
        }
    }
}
{% /tab %}
{% /code %}