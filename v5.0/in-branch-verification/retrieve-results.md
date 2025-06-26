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

After the user has completed their in-branch session you will then be able to retrieve the result of the IBV session. 

Each session has a configured 'time to live' (TTL) which must be above 300 seconds (5 minutes). When a session is created, it remains active until it's time to live is reached. For any active session, you can use the Yoti API to retrieve a report on the session (containing all the end-user's uploaded documents and associated metadata). If you wish to be notified on the progress of the session please use notifications. 

This sections explains how to:

- Retrieve the results of the session

If you would like information on retrieving the ID document images, user information and the report head [here](/identity-verification/results). 

{% code %}
{% tab language="http" %}
GET https://api.yoti.com/session/<sessionId>/configuration
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