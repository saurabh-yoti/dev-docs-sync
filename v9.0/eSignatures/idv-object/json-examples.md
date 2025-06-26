---
type: page
title: JSON Examples
listed: true
slug: json-examples
description: 
index_title: JSON Examples
hidden: 
keywords: 
tags: 
---

### Real Estate

{% code %}
{% tab language="json" %}
{
  "client_session_token_ttl": 604800,
  "resources_ttl": 2630000,
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
      "type": "WATCHLIST_SCREENING",
      "config": {
        "categories": [
          "SANCTIONS",
          "ADVERSE-MEDIA"
        ]
      }
    }
  ],
  "requested_tasks": [
    {
      "type": "ID_DOCUMENT_TEXT_DATA_EXTRACTION",
      "config": {
        "manual_check": "FALLBACK"
      }
    },
    {
      "type": "SUPPLEMENTARY_DOCUMENT_TEXT_DATA_EXTRACTION",
      "config": {
        "manual_check": "FALLBACK"
      }
    }
  ],
  "required_documents": [
    {
      "type": "ID_DOCUMENT"
    },
    {
      "type": "SUPPLEMENTARY_DOCUMENT",
      "document_types": [
        "COUNCIL_TAX_BILL",
        "PHONE_BILL",
        "UTILITY_BILL",
        "BANK_STATEMENT"
      ],
      "objective": {
        "type": "PROOF_OF_ADDRESS"
      }
    }
  ]
}
{% /tab %}
{% /code %}

### HR

{% code %}
{% tab language="json" %}
{
  "client_session_token_ttl": 604800,
  "resources_ttl": 2630000,
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
    }
  ],
  "requested_tasks": [
    {
      "type": "ID_DOCUMENT_TEXT_DATA_EXTRACTION",
      "config": {
        "manual_check": "FALLBACK"
      }
    }
  ]
}
{% /tab %}
{% /code %}

### Finance

{% code %}
{% tab language="json" %}
{
  "client_session_token_ttl": 604800,
  "resources_ttl": 2630000,
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
      "type": "WATCHLIST_SCREENING",
      "config": {
        "categories": [
          "SANCTIONS",
          "ADVERSE-MEDIA"
        ]
      }
    }
  ],
  "requested_tasks": [
    {
      "type": "ID_DOCUMENT_TEXT_DATA_EXTRACTION",
      "config": {
        "manual_check": "FALLBACK"
      }
    },
    {
      "type": "SUPPLEMENTARY_DOCUMENT_TEXT_DATA_EXTRACTION",
      "config": {
        "manual_check": "FALLBACK"
      }
    }
  ],
  "required_documents": [
    {
      "type": "SUPPLEMENTARY_DOCUMENT",
      "document_types": [
        "COUNCIL_TAX_BILL",
        "PHONE_BILL",
        "UTILITY_BILL",
        "BANK_STATEMENT"
      ],
      "objective": {
        "type": "PROOF_OF_ADDRESS"
      }
    }
  ]
}
{% /tab %}
{% /code %}

### Adult

{% code %}
{% tab language="json" %}
{
  "client_session_token_ttl": 604800,
  "resources_ttl": 2630000,
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
    }
  ],
  "requested_tasks": [
    {
      "type": "ID_DOCUMENT_TEXT_DATA_EXTRACTION",
      "config": {
        "manual_check": "FALLBACK"
      }
    }
  ]
}
{% /tab %}
{% /code %}

### Recruitment

{% code %}
{% tab language="json" %}
{
  "client_session_token_ttl": 604800,
  "resources_ttl": 2630000,
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
    }
  ],
  "requested_tasks": [
    {
      "type": "ID_DOCUMENT_TEXT_DATA_EXTRACTION",
      "config": {
        "manual_check": "FALLBACK"
      }
    }
  ]
}
{% /tab %}
{% /code %}

### Liveness Only

{% code %}
{% tab language="json" %}
{
    "client_session_token_ttl": 604800,
    "resources_ttl": 1209600,
    "requested_checks": [
        {
            "type": "LIVENESS",
            "config": {
                "liveness_type": "STATIC",
                "max_retries": 3
            }
        }
    ],
    "sdk_config": {
        "block_biometric_consent": false,
        "allow_handoff": false
    }
}
{% /tab %}
{% /code %}

---