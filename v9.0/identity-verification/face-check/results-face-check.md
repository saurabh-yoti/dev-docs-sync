---
type: page
title: Retrieve results
listed: true
slug: results-face-check
description: 
index_title: Retrieve results
hidden: 
keywords: 
tags: 
---

## Face Check Results

The response will detail the session results information including check and task completion status, resource and media data, along with the associated media identifiers.

### Endpoint

{% code %}
{% tab language="http" %}
GET https://api.yoti.com/idverify/v1/sessions/<SESSION_ID>
{% /tab %}
{% /code %}

When the above endpoint is hit you will receive the results of all checks configured in the session, including the familiar face search check. The response will follow the below format.

#### Response body

{% code %}
{% tab language="json" %}
{
    "client_session_token_ttl": 0,
    "session_id": "7938ac1e-0a4a-49b7-953f-08cfa764358f",
    "state": "COMPLETED",
    "resources": {
        "id_documents": [
            {
                "id": "02ffe8d4-5f4a-4aaa-a046-21593944e05f",
                "tasks": [
                    {
                        "type": "ID_DOCUMENT_TEXT_DATA_EXTRACTION",
                        "id": "1890a33a-1c9e-47f5-88d1-52ff06854e76",
                        "state": "DONE",
                        "created": "2025-06-04T08:49:53Z",
                        "last_updated": "2025-06-04T08:50:39Z",
                        "generated_checks": [],
                        "generated_media": [
                            {
                                "id": "3943b63a-acf6-4860-9984-b73616007046",
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
                "created_at": "2025-06-04T08:49:53Z",
                "last_updated": "2025-06-04T08:50:39Z",
                "document_type": "PASSPORT",
                "issuing_country": "GBR",
                "pages": [
                    {
                        "capture_method": "CAMERA",
                        "media": {
                            "id": "fa453d19-32d1-467d-adb9-44ed2dcb6783",
                            "type": "IMAGE",
                            "created": "2025-06-04T08:50:30Z",
                            "last_updated": "2025-06-04T08:50:30Z"
                        },
                        "frames": [
                            {
                                "media": {
                                    "id": "29a8110f-3eb6-496a-a2ee-5fc56a9758ac",
                                    "type": "IMAGE",
                                    "created": "2025-06-04T08:50:32Z",
                                    "last_updated": "2025-06-04T08:50:32Z"
                                }
                            },
                            {
                                "media": {
                                    "id": "5db33604-3616-457e-80fe-e44af11df8ba",
                                    "type": "IMAGE",
                                    "created": "2025-06-04T08:50:32Z",
                                    "last_updated": "2025-06-04T08:50:32Z"
                                }
                            },
                            {
                                "media": {
                                    "id": "aefacec4-087b-41e0-ab2c-567fbad9d343",
                                    "type": "IMAGE",
                                    "created": "2025-06-04T08:50:32Z",
                                    "last_updated": "2025-06-04T08:50:32Z"
                                }
                            }
                        ]
                    }
                ],
                "document_fields": {
                    "media": {
                        "id": "3943b63a-acf6-4860-9984-b73616007046",
                        "type": "JSON",
                        "created": "2025-06-04T08:50:39Z",
                        "last_updated": "2025-06-04T08:50:39Z"
                    }
                },
                "document_id_photo": {
                    "media": {
                        "id": "a106c265-80d3-4998-8a77-3ccbc3f29ccd",
                        "type": "IMAGE",
                        "created": "2025-06-04T08:50:39Z",
                        "last_updated": "2025-06-04T08:50:39Z"
                    }
                }
            }
        ],
        "supplementary_documents": [],
        "liveness_capture": [
            {
                "id": "e3d4ce28-4291-4dd4-a650-33fd5c3b0e0f",
                "tasks": [],
                "source": {
                    "type": "END_USER"
                },
                "created_at": "2025-06-04T08:50:45Z",
                "last_updated": "2025-06-04T08:51:00Z",
                "image": {
                    "media": {
                        "id": "d12ad6f6-2d1e-4b0d-9650-a153478c7d6e",
                        "type": "IMAGE",
                        "created": "2025-06-04T08:51:00Z",
                        "last_updated": "2025-06-04T08:51:00Z"
                    }
                },
                "liveness_type": "STATIC"
            }
        ],
        "face_capture": [],
        "applicant_profiles": []
    },
    "checks": [
        {
            "type": "LIVENESS",
            "id": "b1e04326-6bba-4a4e-97c5-7191d60c17d9",
            "state": "DONE",
            "resources_used": [
                "e3d4ce28-4291-4dd4-a650-33fd5c3b0e0f"
            ],
            "generated_media": [],
            "report": {
                "recommendation": {
                    "value": "APPROVE"
                },
                "breakdown": [
                    {
                        "sub_check": "face_processing",
                        "result": "PASS",
                        "details": [],
                        "process": "AUTOMATED"
                    },
                    {
                        "sub_check": "liveness_auth",
                        "result": "PASS",
                        "details": [],
                        "process": "AUTOMATED"
                    },
                    {
                        "sub_check": "payload_signature_verification",
                        "result": "PASS",
                        "details": [],
                        "process": "AUTOMATED"
                    }
                ]
            },
            "created": "2025-06-04T08:51:00Z",
            "last_updated": "2025-06-04T08:51:02Z"
        },
        {
            "type": "FAMILIAR_FACE_SEARCH",
            "id": "c9f2b0c0-df4d-472a-93cb-3f93c7ad9196",
            "state": "DONE",
            "resources_used": [
                "e3d4ce28-4291-4dd4-a650-33fd5c3b0e0f"
            ],
            "generated_media": [],
            "report": {
                "recommendation": {
                    "value": "REJECT",
                    "reason": "MATCH_FOUND"
                },
                "breakdown": [
                    {
                        "sub_check": "face_not_found_in_pool",
                        "result": "FAIL",
                        "details": [
                            {
                                "name": "matching_pool",
                                "value": "a8b2e5de-a31f-4e82-b2ac-557a492fa88e"
                            },
                            {
                                "name": "matching_applicant",
                                "value": "b1ac68ca-c692-449f-b6cc-1ee7c0d366ea"
                            }
                        ],
                        "process": "AUTOMATED"
                    }
                ]
            },
            "created": "2025-06-04T08:51:03Z",
            "last_updated": "2025-06-04T08:51:05Z",
            "config": {
                "pool_id": "a8b2e5de-a31f-4e82-b2ac-557a492fa88e",
                "pool_label": "POOL EXAMPLE",
                "approval_criteria": "NO_MATCH"
            }
        }
    ],
    "user_tracking_id": "<YOUR_USER_ID>",
    "biometric_consent": "2025-06-04T08:50:43Z"
}
{% /tab %}
{% /code %}

Within the **Familiar Face Search** check object you will details regarding the result of the check. The recommendation value will depend upon what has been configured in the "approval_criteria"_._ If the approval criteria is set to "MATCH" the recommendation value will be APPROVE if there is a match and if approval_criteria is set to "NO MATCH" the recommendation value will be APPROVE if there is not a match. The Familiar Face Search check object will also detail the applicant pool id that is being searched against as well as a list of applicant ids.