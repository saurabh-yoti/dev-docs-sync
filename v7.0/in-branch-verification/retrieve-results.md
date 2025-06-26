---
type: page
title: Retrieve results
listed: false
slug: retrieve-results
description: 
index_title: Retrieve results
hidden: 
keywords: 
tags: 
---

After the user has completed their session you will then be able to retrieve the result of the session. 

For any active session, you can use the Yoti API to retrieve a report on the session (containing all the end-user's uploaded documents, and recommendations). If you wish to be notified on the progress of the session please use notifications. 

This sections explains how to:

- Retrieve the results of the session

If you would like information on retrieving the ID document images, user information and the report head [here](/identity-verification/results). 

{% code %}
{% tab language="http" %}
GET https://api.yoti.com/idverify/v1/sessions/{sessionId}
{% /tab %}
{% /code %}

Example of the get session response of a completed session, outlining the state of the checks. A recommendation value of "APPROVE" will be issued for each one. The person in branch will not complete the session if:

- All / Any of the documents are not present
- The profile data doesn't match
- If the wrong documents are brought in
- If the documents are not valid

{% code %}
{% tab language="json" %}
{
  "session_id": "3fa85f64-5717-4562-b3fc-2c963f66afa6",
  "resources": {
    "id_documents": [
      {
        "id": "aaaaaaa-5717-4562-b3fc-2c963f66afa6",
        "source": { "type": "IBV" },
        "document_type": "PASSPORT",
        "issuing_country": "GBR",
        "pages": [],
        "tasks": []
      }
    ],
    "supplementary_documents": [
      {
        "id": "bbbbbb-5717-4562-b3fc-2c963f66afa6",
        "source": { "type": "IBV" },
        "document_type": "UTILITY_BILL",
        "issuing_country": "GBR",
        "file": { },
        "pages": [],
        "tasks": []
      }
    ],
    "applicant_profile": {
      "id": "ccccccc-5717-4562-b3fc-2c963f66afa6",
      "source": { "type": "RELYING_BUSINESS" },
      "media": {
        "id": "3fa85f64-5717-4562-b3fc-2c963f66afa6",
        "type": "JSON",
        "created": "2021-06-11T11:39:24Z",
        "last_updated": "2021-06-11T11:39:24Z"
      }
    }
  },
  "checks": [
    {
      "id": "3fa85f64-5717-4562-b3fc-2c963f66afa6",
      "type": "IBV_VISUAL_REVIEW_CHECK",
      "state": "DONE",
      "resources_used": [ "aaaaaaa-5717-4562-b3fc-2c963f66afa6" ],
      "generated_media": [],
      "report": {
        "recommendation": {
          "value": "APPROVE"
        },
        "breakdown": [ ]
      },
      "created": "2021-06-11T11:39:24Z",
      "last_updated": "2021-06-11T11:39:24Z"
    },
    {
      "id": "3fa85f64-5717-4562-b3fc-2c963f66afa6",
      "type": "IBV_VISUAL_REVIEW_CHECK",
      "state": "DONE",
      "resources_used": [ "bbbbbb-5717-4562-b3fc-2c963f66afa6"],
      "generated_media": [],
      "report": {
        "recommendation": {
          "value": "APPROVE"
        },
        "breakdown": [ ]
      },
      "created": "2021-06-11T11:39:24Z",
      "last_updated": "2021-06-11T11:39:24Z"
    },
    {
      "id": "3fa85f64-5717-4562-b3fc-2c963f66afa6",
      "type": "DOCUMENT_SCHEME_VALIDITY_CHECK",
      "state": "DONE",
      "resources_used": [ "aaaaaaa-5717-4562-b3fc-2c963f66afa6" ],
      "generated_media": [],
      "report": {
        "recommendation": {
          "value": "APPROVE"
        },
        "breakdown": [ ]
      },
      "created": "2021-06-11T11:39:24Z",
      "last_updated": "2021-06-11T11:39:24Z"
    },
    {
      "id": "3fa85f64-5717-4562-b3fc-2c963f66afa6",
      "type": "DOCUMENT_SCHEME_VALIDITY_CHECK",
      "state": "DONE",
      "resources_used": [ "bbbbbb-5717-4562-b3fc-2c963f66afa6"],
      "generated_media": [],
      "report": {
        "recommendation": {
          "value": "APPROVE"
        },
        "breakdown": [ ]
      },
      "created": "2021-06-11T11:39:24Z",
      "last_updated": "2021-06-11T11:39:24Z"
    },
    {
      "id": "3fa85f64-5717-4562-b3fc-2c963f66afa6",
      "type": "PROFILE_DOCUMENT_MATCH",
      "state": "DONE",
      "resources_used": [ "aaaaaaa-5717-4562-b3fc-2c963f66afa6", "ccccccc-5717-4562-b3fc-2c963f66afa6"        ],
      "generated_media": [],
      "report": {
        "recommendation": {
          "value": "APPROVE"
        },
        "breakdown": [ ]
      },

      "created": "2021-06-11T11:39:24Z",
      "last_updated": "2021-06-11T11:39:24Z"
    },
    {
      "id": "3fa85f64-5717-4562-b3fc-2c963f66afa6",
      "type": "PROFILE_DOCUMENT_MATCH",
      "state": "DONE",
      "resources_used": [ "bbbbbb-5717-4562-b3fc-2c963f66afa6", "ccccccc-5717-4562-b3fc-2c963f66afa6"          ],
      "generated_media": [],
      "report": {
        "recommendation": {
          "value": "APPROVE"
        },
        "breakdown": [ ]
      },

      "created": "2021-06-11T11:39:24Z",
      "last_updated": "2021-06-11T11:39:24Z"
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