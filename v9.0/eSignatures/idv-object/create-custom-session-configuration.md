---
type: page
title: Create Custom Session Configuration
listed: true
slug: create-custom-session-configuration
description: 
index_title: Create Custom Session Configuration
hidden: 
keywords: 
tags: 
---

You can use this endpoint to create your own custom made identity verification session configuration. 

{% code %}
{% tab language="http" %}
POST https://api.yotisign.com/v2/idv/sessions/configs
{% /tab %}
{% /code %}

---

### Headers Explained

The following elements are needed:

{% table %}
| Header | Description | 
| ---- | ---- | 
| Authorization (header) | API Key to call the Yoti Sign API. This should be sent as a bearer token. | 
| Content-Type (header) | application/json | 
{% /table %}

---

### Request Payload

An example of the request body can be found below:

{% code %}
{% tab language="json" %}
{
    "name": "My Custom Session config",
    "is_private": false,
    "session_config":
    {
            "client_session_token_ttl": 1200,
            "resources_ttl": 2630000,
            "user_tracking_id": "string",
            "block_biometric_consent": false,
            "requested_checks":
            [
                {
                    "type": "ID_DOCUMENT_AUTHENTICITY",
                    "config":
                    {
                        "manual_check": "FALLBACK"
                    }
                },
                {
                    "type": "LIVENESS",
                    "config":
                    {
                        "liveness_type": "ZOOM",
                        "max_retries": 3
                    }
                },
                {
                    "type": "ID_DOCUMENT_FACE_MATCH",
                    "config":
                    {
                        "manual_check": "FALLBACK"
                    }
                },
                {
                    "type": "WATCHLIST_SCREENING",
                    "config":
                    {
                        "categories":
                        [
                            "SANCTIONS",
                            "ADVERSE-MEDIA"
                        ]
                    }
                },
                {
                    "type": "THIRD_PARTY_IDENTITY",
                    "config":
                    {
                        "manual_check": "NEVER"
                    }
                }
            ],
            "requested_tasks":
            [
                {
                    "type": "ID_DOCUMENT_TEXT_DATA_EXTRACTION",
                    "config":
                    {
                        "manual_check": "FALLBACK"
                    }
                },
                {
                    "type": "SUPPLEMENTARY_DOCUMENT_TEXT_DATA_EXTRACTION",
                    "config":
                    {
                        "manual_check": "FALLBACK"
                    }
                }
            ],
            "required_documents":
            [
                {
                    "type": "ID_DOCUMENT"
                },
                {
                    "type": "SUPPLEMENTARY_DOCUMENT",
                    "document_types":
                    [
                        "COUNCIL_TAX_BILL",
                        "PHONE_BILL",
                        "UTILITY_BILL"
                    ],
                    "objective":
                    {
                        "type": "PROOF_OF_ADDRESS"
                    }
                }
            ]
        }
}
{% /tab %}
{% /code %}

{% table widths="169" %}
| Value | Description | 
| ---- | ---- | 
| name | This is the name of your custom configuration, and will need to be used when specifying which configuration to use. | 
| is_private | Whether to keep this session config as only accessible from this API key, or whether to allow other users of your organisation to use it | 
| session_config | An identity verification payload, to be used to customise the identity verification session. | 
{% /table %}