---
type: page
title: Configure the check
listed: true
slug: configure-face-check
description: 
index_title: Configure the check
hidden: 
keywords: 
tags: 
---

## Configure Face Check

The Final step would be to create an identity verification session while configuring the Face check service. You can continue to use the Request builder to interact with our API.

{% code %}
{% tab language="http" %}
POST https://api.yoti.com/idverify/v1/sessions
{% /tab %}
{% /code %}

### Request body

More details regarding the session creation request can be found here

{% code %}
{% tab language="json" %}
{
  "client_session_token_ttl": 600,
  "resources_ttl": 604800,
  "user_tracking_id": "<YOUR_USER_ID>",
  "notifications": {
    "endpoint": "https://yourdomain.example/idverify/updates",
    "topics": [
      "session_completion"
    ],
    "auth_token": "username:password"
  },
  "requested_checks": [
	{
 		"type": "ID_DOCUMENT_AUTHENTICITY",
		"config": {
       "manual_check": "FALLBACK"
		}
	},
	{
		"type": "LIVENESS",
		"config": {
			"liveness_type": "STATIC",
			"max_retries": 3
		}
	},
	{
		"type": "ID_DOCUMENT_FACE_MATCH",
		"config": {
			"manual_check": "FALLBACK"
		}
	},
  {
    "type": "FAMILIAR_FACE_SEARCH",
    "config": {
      "pool_id": "<applicant pool uuid>",
      "approval_criteria": "MATCH"
      }
    }
  ],
  "requested_tasks": [
    {
      "type": "ID_DOCUMENT_TEXT_DATA_EXTRACTION",
      "config": {
        "manual_check": "FALLBACK"
      }
    }
  ],
  "sdk_config": {
    "allowed_capture_methods": "CAMERA",
    "primary_colour": "#2d9fff",
    "secondary_colour": "#FFFFFF",
    "font_colour": "#FFFFFF",
    "preset_issuing_country": "GBR",
    "success_url": "https://yourdomain.example/success",
    "error_url": "https://yourdomain.example/error"
  }
}
{% /tab %}
{% /code %}

The **"FAMILIAR_FACE_SEARCH"** is the check that needs to be configured for this Face checking service. Within this check there is a config that needs to be provided. The pool_id will correspond with the pool of applicants that has been created, and the approval**_**critera can be set to MATCH or NO_MATCH. If set to MATCH we will approve this check if the user undergoing the session matches one of the applicants in the pool. Whilst if set to NO_ MATCH we will approve this check if the user undergoing the session does not match one of the applicants in the pool.

### Response

If the request is successful and a session is generated the API will send a response in the form:

{% code %}
{% tab language="json" %}
{
  "client_session_token_ttl": 599,
  "client_session_token": "<uuid>",
  "session_id": "<uuid>"
}
{% /tab %}
{% /code %}

---

## Client Side View

The next step is to load the Yoti client-side SDK. To do this, you need the below parameters generated with the session creation request above:

- Session ID
- Session Token

We then utilise these to construct a Web URL which loads the Yoti Client SDK. The URL is in the following format:

{% code %}
{% tab language="http" %}
https://api.yoti.com/idverify/v1/web/index.html?sessionID=<sessionID>&sessionToken=<sessionToken>
{% /tab %}
{% /code %}