---
type: page
title: Retrieve results
listed: true
slug: ibv-retrieve-results
description: 
index_title: Retrieve results
hidden: 
keywords: 
tags: 
---

After the user has completed their in-branch session you will then be able to retrieve the result of the IBV session. 

Each session has a configured 'time to live' (TTL) which must be above 300 seconds (5 minutes). When a session is created, it remains active until it's time to live is reached. For any active session, you can use the Yoti API to retrieve a report on the session (containing all the end-user's uploaded documents and associated metadata). If you wish to be notified on the progress of the session please use notifications. 

This sections explains how to:

- Retrieve the results of the session

If you would like information on retrieving the ID document images, user information and the report head [here](/identity-verification/results). 

{% code %}
{% tab language="http" %}
GET https://api.yoti.com/idverify/v1/session/<sessionId>/configuration
{% /tab %}
{% /code %}

Example of the configured response stating what documentation and checks are required.

{% code %}
{% tab language="javascript" %}
{
  "client_session_token_ttl": 599,
  "session_id": "3fa85f64-5717-4562-b3fc-2c963f66afa6",
  "requested_checks": [ ... ],
  "capture": {
    ...
    "required_resources": [
      {
        "type": "ID_DOCUMENT",
        "id": "3fa85f64-5717-4562-b3fc-2c963f66afa6",
        "state": "REQUIRED",
        ...

        "allowed_sources": [
          { "type": "END_USER" },
          {
            "type": "IBV",
            "allowed_providers": [ "UK_POST_OFFICE" ], 
          }
        ]

      },
      {
        "type": "SUPPLEMENTARY_DOCUMENT",
        "id": "3fa85f64-5717-4562-b3fc-2c963f66afa6",
        "state": "REQUIRED",
        ...

        "allowed_sources": [ ] // exactly as above
      },
      {
        "type": "LIVENESS",
        "id": "3fa85f64-5717-4562-b3fc-2c963f66afa6",
        "liveness_type": "ZOOM",
        "state": "REQUIRED",
        "allowed_sources": [ ] // exactly as above
      },
      {
        "type": "FACE_CAPTURE",
        "id": "3fa85f64-5717-4562-b3fc-2c963f66afa6",
        "state": "REQUIRED",
        "allowed_sources": [
          { "type": "END_USER" },
          { "type": "RELYING_BUSINESS" },
          { "type": "IBV" } // as above
        ]
      }

    ]
  },
  "sdk_config": { }
}
{% /tab %}
{% /code %}

{% badge type="info" text="Hint" /%} Face capture is the result of the image capture of the user. 

{% code %}
{% tab language="http" %}
GET  https://api.yoti.com/idverify/v1/session/<sessionId>/
{% /tab %}
{% /code %}

Example of a response outlining the state of the checks. Once the checks are complete a recommendation value will be issued for each one.

{% code %}
{% tab language="json" %}
{
    "client_session_token_ttl": 8924,
    "session_id": "d6f48ec7-b6ff-4b86-b51e-d96c79ad8a13",
    "state": "ONGOING",
    "resources": {
        "id_documents": [
            {
                "id": "5e1c9917-a7a2-4d25-8f42-c0d712e0dfee",
                "tasks": [
                    {
                        "type": "ID_DOCUMENT_TEXT_DATA_EXTRACTION",
                        "id": "0cf5c9a8-c1ca-49dd-8440-408cd82ff879",
                        "state": "PENDING",
                        "created": "2021-11-23T13:46:05Z",
                        "last_updated": "2021-11-23T13:46:29Z",
                        "generated_checks": [
                            {
                                "id": "8683a83a-cdfc-45a1-8f85-4b09d4814370",
                                "type": "ID_DOCUMENT_TEXT_DATA_CHECK"
                            }
                        ],
                        "generated_media": []
                    }
                ],
                "source": {
                    "type": "END_USER"
                },
                "document_type": "PASSPORT",
                "issuing_country": "USA",
                "pages": [
                    {
                        "capture_method": "CAMERA",
                        "media": {
                            "id": "399c64f2-ad6a-4140-9a9b-8c9f2081d72b",
                            "type": "IMAGE",
                            "created": "2021-11-23T13:46:16Z",
                            "last_updated": "2021-11-23T13:46:16Z"
                        },
                        "frames": [
                            {
                                "media": {
                                    "id": "f3be5382-1cb6-4b95-bb4a-713b49a6bbbc",
                                    "type": "IMAGE",
                                    "created": "2021-11-23T13:46:18Z",
                                    "last_updated": "2021-11-23T13:46:18Z"
                                }
                            },
                            {
                                "media": {
                                    "id": "54446131-1b23-4dd8-a42e-d6634ac72379",
                                    "type": "IMAGE",
                                    "created": "2021-11-23T13:46:20Z",
                                    "last_updated": "2021-11-23T13:46:20Z"
                                }
                            },
                            {
                                "media": {
                                    "id": "41edd345-8207-47e0-9e98-17a0382be739",
                                    "type": "IMAGE",
                                    "created": "2021-11-23T13:46:20Z",
                                    "last_updated": "2021-11-23T13:46:20Z"
                                }
                            }
                        ]
                    }
                ]
            },
            {
                "id": "5f709804-9995-4d98-b8d5-41818c05d9fe",
                "tasks": [
                    {
                        "type": "ID_DOCUMENT_TEXT_DATA_EXTRACTION",
                        "id": "a98b3f7a-2bfc-4067-9357-6f13662eb02a",
                        "state": "FAILED",
                        "created": "2021-11-23T13:45:42Z",
                        "last_updated": "2021-11-23T13:46:03Z",
                        "generated_checks": [],
                        "generated_media": []
                    }
                ],
                "source": {
                    "type": "END_USER"
                },
                "document_type": "PASSPORT",
                "issuing_country": "USA",
                "pages": [
                    {
                        "capture_method": "CAMERA",
                        "media": {
                            "id": "d601e48d-78ee-4266-a4a2-1b13c37bf769",
                            "type": "IMAGE",
                            "created": "2021-11-23T13:45:56Z",
                            "last_updated": "2021-11-23T13:45:56Z"
                        },
                        "frames": [
                            {
                                "media": {
                                    "id": "6a189760-1d43-4806-ae1d-806f5425eb77",
                                    "type": "IMAGE",
                                    "created": "2021-11-23T13:45:57Z",
                                    "last_updated": "2021-11-23T13:45:57Z"
                                }
                            },
                            {
                                "media": {
                                    "id": "a4b326f3-ec1d-4191-bcc2-77972499b32f",
                                    "type": "IMAGE",
                                    "created": "2021-11-23T13:45:58Z",
                                    "last_updated": "2021-11-23T13:45:58Z"
                                }
                            },
                            {
                                "media": {
                                    "id": "f41d2d34-f3ec-45b0-9b00-500bbe808a52",
                                    "type": "IMAGE",
                                    "created": "2021-11-23T13:45:58Z",
                                    "last_updated": "2021-11-23T13:45:58Z"
                                }
                            }
                        ]
                    }
                ]
            }
        ],
        "supplementary_documents": [],
        "liveness_capture": [],
        "face_capture": []
    },
    "checks": [
        {
            "type": "ID_DOCUMENT_AUTHENTICITY",
            "id": "d6793869-27ac-478e-b9b1-fdec58291b6b",
            "state": "READY",
            "resources_used": [
                "5e1c9917-a7a2-4d25-8f42-c0d712e0dfee"
            ],
            "generated_media": [],
            "created": "2021-11-23T13:46:30Z",
            "last_updated": "2021-11-23T13:46:30Z"
        },
        {
            "type": "ID_DOCUMENT_TEXT_DATA_CHECK",
            "id": "8683a83a-cdfc-45a1-8f85-4b09d4814370",
            "state": "PENDING",
            "resources_used": [
                "5e1c9917-a7a2-4d25-8f42-c0d712e0dfee"
            ],
            "generated_media": [],
            "created": "2021-11-23T13:46:30Z",
            "last_updated": "2021-11-23T13:46:30Z"
        }
    ]
}
{% /tab %}
{% /code %}

The following is present in every session result. 

{% table widths="267" %}
| Value | Description | 
| ---- | ---- | 
| Resources | A container of all ID documents and liveness captures for this session. | 
| Checks | A container of all checks performed for this session | 
{% /table %}