---
type: page
title: Get IDV Session Result
listed: true
slug: get-idv-session-result
description: 
index_title: Get IDV Session Result
hidden: 
keywords: 
tags: 
---

This endpoint will return the result of the Identity verification session in JSON format.

{% badge type="success" text="Hint" /%}If a recipient successfully signed the document but was unable to complete a session due to a technical problem (like a problem with their camera), the session status will be ONGOING.

{% badge type="error" text="Important" /%} If the recipient needs to attempt IDV again the sender must resend the envelope.

{% code %}
{% tab language="http" %}
GET https://api.yotisign.com/v2/idv/recipients/:recipientID/sessions/signed/json
{% /tab %}
{% /code %}

---

## Headers Explained

The following elements are needed:

{% table widths="228" %}
| Header | Description | 
| ---- | ---- | 
| Authorization | API Key to call the Yoti Sign API. This should be sent as a bearer token. | 
{% /table %}

---

### Response

On success, we return a 200 with a JSON body matching the following schema:

{% code %}
{% tab language="json" %}
{
  "session_id": "3fa85f64-5717-4562-b3fc-2c963f66afa6",
  "client_session_token_ttl": 599,
  "user_tracking_id": "string",
  "biometric_consent": "2022-12-01T15:23:28.894Z",
  "state": "ONGOING",
  "client_session_token": "3fa85f64-5717-4562-b3fc-2c963f66afa6",
  "resources": {
    "id_documents": [
      {
        "id": "3fa85f64-5717-4562-b3fc-2c963f66afa6",
        "source": {
          "type": "END_USER"
        },
        "document_type": "string",
        "issuing_country": "string",
        "pages": [
          {
            "capture_method": "CAMERA",
            "media": {
              "id": "3fa85f64-5717-4562-b3fc-2c963f66afa6",
              "type": "IMAGE",
              "created": "2021-06-11T11:39:24Z",
              "last_updated": "2021-06-11T11:39:24Z"
            },
            "frames": [
              {
                "media": {
                  "id": "3fa85f64-5717-4562-b3fc-2c963f66afa6",
                  "type": "IMAGE",
                  "created": "2021-06-11T11:39:24Z",
                  "last_updated": "2021-06-11T11:39:24Z"
                }
              }
            ]
          }
        ],
        "document_fields": {
          "media": {
            "id": "3fa85f64-5717-4562-b3fc-2c963f66afa6",
            "type": "IMAGE",
            "created": "2021-06-11T11:39:24Z",
            "last_updated": "2021-06-11T11:39:24Z"
          }
        },
        "document_id_photo": {
          "media": {
            "id": "3fa85f64-5717-4562-b3fc-2c963f66afa6",
            "type": "IMAGE",
            "created": "2021-06-11T11:39:24Z",
            "last_updated": "2021-06-11T11:39:24Z"
          }
        },
        "tasks": [
          {
            "id": "3fa85f64-5717-4562-b3fc-2c963f66afa6",
            "state": "DONE",
            "created": "2021-06-11T11:39:24Z",
            "last_updated": "2021-06-11T11:39:24Z",
            "generated_media": [
              {
                "id": "3fa85f64-5717-4562-b3fc-2c963f66afa6",
                "type": "IMAGE"
              }
            ],
            "generated_checks": [
              {
                "id": "3fa85f64-5717-4562-b3fc-2c963f66afa6",
                "type": "ID_DOCUMENT_TEXT_DATA_CHECK"
              }
            ],
            "type": "ID_DOCUMENT_TEXT_DATA_EXTRACTION"
          }
        ]
      }
    ],
    "supplementary_documents": [
      {
        "id": "3fa85f64-5717-4562-b3fc-2c963f66afa6",
        "source": {
          "type": "END_USER"
        },
        "document_type": "string",
        "issuing_country": "string",
        "file": {
          "media": {
            "id": "3fa85f64-5717-4562-b3fc-2c963f66afa6",
            "type": "IMAGE",
            "created": "2021-06-11T11:39:24Z",
            "last_updated": "2021-06-11T11:39:24Z"
          }
        },
        "pages": [
          {
            "capture_method": "CAMERA",
            "media": {
              "id": "3fa85f64-5717-4562-b3fc-2c963f66afa6",
              "type": "IMAGE",
              "created": "2021-06-11T11:39:24Z",
              "last_updated": "2021-06-11T11:39:24Z"
            },
            "frames": [
              {
                "media": {
                  "id": "3fa85f64-5717-4562-b3fc-2c963f66afa6",
                  "type": "IMAGE",
                  "created": "2021-06-11T11:39:24Z",
                  "last_updated": "2021-06-11T11:39:24Z"
                }
              }
            ]
          }
        ],
        "document_fields": {
          "media": {
            "id": "3fa85f64-5717-4562-b3fc-2c963f66afa6",
            "type": "IMAGE",
            "created": "2021-06-11T11:39:24Z",
            "last_updated": "2021-06-11T11:39:24Z"
          }
        },
        "tasks": [
          {
            "id": "3fa85f64-5717-4562-b3fc-2c963f66afa6",
            "state": "DONE",
            "created": "2021-06-11T11:39:24Z",
            "last_updated": "2021-06-11T11:39:24Z",
            "generated_media": [
              {
                "id": "3fa85f64-5717-4562-b3fc-2c963f66afa6",
                "type": "IMAGE"
              }
            ],
            "generated_checks": [
              {
                "id": "3fa85f64-5717-4562-b3fc-2c963f66afa6",
                "type": "ID_DOCUMENT_TEXT_DATA_CHECK"
              }
            ],
            "type": "SUPPLEMENTARY_DOCUMENT_TEXT_DATA_EXTRACTION"
          }
        ]
      }
    ],
    "liveness_capture": [
      {
        "id": "3fa85f64-5717-4562-b3fc-2c963f66afa6",
        "source": {
          "type": "END_USER"
        },
        "liveness_type": "ZOOM",
        "facemap": {
          "media": {
            "id": "3fa85f64-5717-4562-b3fc-2c963f66afa6",
            "type": "IMAGE",
            "created": "2021-06-11T11:39:24Z",
            "last_updated": "2021-06-11T11:39:24Z"
          }
        },
        "frames": [
          {
            "media": {
              "id": "3fa85f64-5717-4562-b3fc-2c963f66afa6",
              "type": "IMAGE",
              "created": "2021-06-11T11:39:24Z",
              "last_updated": "2021-06-11T11:39:24Z"
            }
          }
        ],
        "tasks": []
      }
    ],
    "face_capture": [
      {
        "id": "3fa85f64-5717-4562-b3fc-2c963f66afa6",
        "source": {
          "type": "END_USER"
        },
        "image": {
          "media": {
            "id": "3fa85f64-5717-4562-b3fc-2c963f66afa6",
            "type": "IMAGE",
            "created": "2021-06-11T11:39:24Z",
            "last_updated": "2021-06-11T11:39:24Z"
          }
        },
        "tasks": []
      }
    ]
  },
  "checks": [
    {
      "id": "3fa85f64-5717-4562-b3fc-2c963f66afa6",
      "type": "ID_DOCUMENT_AUTHENTICITY",
      "state": "CREATED",
      "resources_used": [
        "3fa85f64-5717-4562-b3fc-2c963f66afa6"
      ],
      "generated_media": [
        {
          "id": "3fa85f64-5717-4562-b3fc-2c963f66afa6",
          "type": "IMAGE"
        }
      ],
      "report": {
        "recommendation": {
          "value": "APPROVE"
        },
        "breakdown": [
          {
            "sub_check": "string",
            "result": "PASS",
            "details": []
          }
        ]
      },
      "created": "2021-06-11T11:39:24Z",
      "last_updated": "2021-06-11T11:39:24Z"
    },
    {
      "id": "3fa85f64-5717-4562-b3fc-2c963f66afa6",
      "type": "ID_DOCUMENT_TEXT_DATA_CHECK",
      "state": "CREATED",
      "resources_used": [
        "3fa85f64-5717-4562-b3fc-2c963f66afa6"
      ],
      "generated_media": [
        {
          "id": "3fa85f64-5717-4562-b3fc-2c963f66afa6",
          "type": "IMAGE"
        }
      ],
      "report": {
        "recommendation": {
          "value": "APPROVE"
        },
        "breakdown": [
          {
            "sub_check": "string",
            "result": "PASS",
            "details": []
          }
        ]
      },
      "created": "2021-06-11T11:39:24Z",
      "last_updated": "2021-06-11T11:39:24Z"
    },
    {
      "id": "3fa85f64-5717-4562-b3fc-2c963f66afa6",
      "type": "LIVENESS",
      "state": "CREATED",
      "resources_used": [
        "3fa85f64-5717-4562-b3fc-2c963f66afa6"
      ],
      "generated_media": [
        {
          "id": "3fa85f64-5717-4562-b3fc-2c963f66afa6",
          "type": "IMAGE"
        }
      ],
      "report": {
        "recommendation": {
          "value": "APPROVE"
        },
        "breakdown": [
          {
            "sub_check": "string",
            "result": "PASS",
            "details": []
          }
        ]
      },
      "created": "2021-06-11T11:39:24Z",
      "last_updated": "2021-06-11T11:39:24Z"
    },
    {
      "id": "3fa85f64-5717-4562-b3fc-2c963f66afa6",
      "type": "ID_DOCUMENT_FACE_MATCH",
      "state": "CREATED",
      "resources_used": [
        "3fa85f64-5717-4562-b3fc-2c963f66afa6"
      ],
      "generated_media": [
        {
          "id": "3fa85f64-5717-4562-b3fc-2c963f66afa6",
          "type": "IMAGE"
        }
      ],
      "report": {
        "recommendation": {
          "value": "APPROVE"
        },
        "breakdown": [
          {
            "sub_check": "string",
            "result": "PASS",
            "details": []
          }
        ]
      },
      "created": "2021-06-11T11:39:24Z",
      "last_updated": "2021-06-11T11:39:24Z"
    },
    {
      "id": "3fa85f64-5717-4562-b3fc-2c963f66afa6",
      "type": "ID_DOCUMENT_COMPARISON",
      "state": "CREATED",
      "resources_used": [
        "3fa85f64-5717-4562-b3fc-2c963f66afa6"
      ],
      "generated_media": [
        {
          "id": "3fa85f64-5717-4562-b3fc-2c963f66afa6",
          "type": "IMAGE"
        }
      ],
      "report": {
        "recommendation": {
          "value": "APPROVE"
        },
        "breakdown": [
          {
            "sub_check": "string",
            "result": "PASS",
            "details": []
          }
        ]
      },
      "created": "2021-06-11T11:39:24Z",
      "last_updated": "2021-06-11T11:39:24Z"
    },
    {
      "id": "3fa85f64-5717-4562-b3fc-2c963f66afa6",
      "type": "THIRD_PARTY_IDENTITY",
      "state": "CREATED",
      "resources_used": [
        "3fa85f64-5717-4562-b3fc-2c963f66afa6"
      ],
      "generated_media": [
        {
          "id": "3fa85f64-5717-4562-b3fc-2c963f66afa6",
          "type": "IMAGE"
        }
      ],
      "generated_profile": {
        "media": {
          "id": "3fa85f64-5717-4562-b3fc-2c963f66afa6",
          "type": "IMAGE",
          "created": "2021-06-11T11:39:24Z",
          "last_updated": "2021-06-11T11:39:24Z"
        }
      },
      "report": {
        "recommendation": {
          "value": "APPROVE"
        },
        "breakdown": [
          {
            "sub_check": "string",
            "result": "PASS",
            "details": []
          }
        ]
      },
      "created": "2021-06-11T11:39:24Z",
      "last_updated": "2021-06-11T11:39:24Z"
    },
    {
      "id": "3fa85f64-5717-4562-b3fc-2c963f66afa6",
      "type": "WATCHLIST_SCREENING",
      "state": "CREATED",
      "resources_used": [
        "3fa85f64-5717-4562-b3fc-2c963f66afa6"
      ],
      "generated_media": [
        {
          "id": "3fa85f64-5717-4562-b3fc-2c963f66afa6",
          "type": "IMAGE"
        }
      ],
      "generated_profile": {
        "media": {
          "id": "3fa85f64-5717-4562-b3fc-2c963f66afa6",
          "type": "IMAGE",
          "created": "2021-06-11T11:39:24Z",
          "last_updated": "2021-06-11T11:39:24Z"
        }
      },
      "report": {
        "recommendation": {
          "value": "APPROVE"
        },
        "breakdown": [
          {
            "sub_check": "string",
            "result": "PASS",
            "details": []
          }
        ],
        "watchlist_summary": {
          "total_hits": 0,
          "search_config": {
            "categories": [
              "ADVERSE-MEDIA"
            ]
          },
          "raw_results": {
            "media": {
              "id": "3fa85f64-5717-4562-b3fc-2c963f66afa6",
              "type": "IMAGE",
              "created": "2021-06-11T11:39:24Z",
              "last_updated": "2021-06-11T11:39:24Z"
            }
          },
          "associated_country_codes": [
            "GBR",
            "USA"
          ]
        }
      },
      "created": "2021-06-11T11:39:24Z",
      "last_updated": "2021-06-11T11:39:24Z"
    },
    {
      "id": "3fa85f64-5717-4562-b3fc-2c963f66afa6",
      "type": "WATCHLIST_ADVANCED_CA",
      "state": "CREATED",
      "resources_used": [
        "3fa85f64-5717-4562-b3fc-2c963f66afa6"
      ],
      "generated_media": [
        {
          "id": "3fa85f64-5717-4562-b3fc-2c963f66afa6",
          "type": "IMAGE"
        }
      ],
      "generated_profile": {
        "media": {
          "id": "3fa85f64-5717-4562-b3fc-2c963f66afa6",
          "type": "IMAGE",
          "created": "2021-06-11T11:39:24Z",
          "last_updated": "2021-06-11T11:39:24Z"
        }
      },
      "report": {
        "recommendation": {
          "value": "APPROVE"
        },
        "breakdown": [
          {
            "sub_check": "string",
            "result": "PASS",
            "details": []
          }
        ],
        "watchlist_summary": {
          "total_hits": 0,
          "search_config": {
            "categories": [
              "ADVERSE-MEDIA"
            ]
          },
          "raw_results": {
            "media": {
              "id": "3fa85f64-5717-4562-b3fc-2c963f66afa6",
              "type": "IMAGE",
              "created": "2021-06-11T11:39:24Z",
              "last_updated": "2021-06-11T11:39:24Z"
            }
          },
          "associated_country_codes": [
            "GBR",
            "USA"
          ]
        }
      },
      "created": "2021-06-11T11:39:24Z",
      "last_updated": "2021-06-11T11:39:24Z"
    },
    {
      "id": "3fa85f64-5717-4562-b3fc-2c963f66afa6",
      "type": "SUPPLEMENTARY_DOCUMENT_TEXT_DATA_CHECK",
      "state": "CREATED",
      "resources_used": [
        "3fa85f64-5717-4562-b3fc-2c963f66afa6"
      ],
      "generated_media": [
        {
          "id": "3fa85f64-5717-4562-b3fc-2c963f66afa6",
          "type": "IMAGE"
        }
      ],
      "report": {
        "recommendation": {
          "value": "APPROVE"
        },
        "breakdown": [
          {
            "sub_check": "string",
            "result": "PASS",
            "details": []
          }
        ]
      },
      "created": "2021-06-11T11:39:24Z",
      "last_updated": "2021-06-11T11:39:24Z"
    }
  ]
}
{% /tab %}
{% /code %}

---

## Error codes

If the request is unsuccessful we will respond with an appropriate HTTP code, and a message will be detailed in the response body.