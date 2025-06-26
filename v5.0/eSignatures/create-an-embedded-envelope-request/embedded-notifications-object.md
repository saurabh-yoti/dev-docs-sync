---
type: page
title: Notifications object
listed: true
slug: embedded-notifications-object
description: 
index_title: Notifications object
hidden: 
keywords: 
tags: 
---

You can subscribe to notifications which will be sent to a specified endpoint. This endpoint will need to be publicly accessible.

{% code %}
{% tab language="json" %}
"notifications": {
        "destination": "https://mysite.com/events",
        "subscriptions": [
            "envelope_completion"
            "envelope_ready"
            "signer_completion"
   
       ]
    }
{% /tab %}
{% /code %}

{% table %}
| Parameter | Description | 
| ---- | ---- | 
| destination | scheme of the URL must be HTTPS and a discrete parameter | 
| envelope_completion | When ever a user signs Yoti will send the envelope id and the recipient id that has signed. | 
| envelope_ready | Emitted from the gateway at the time the document is sealed. | 
| signer_completion | The signer has signed. | 
| upload_errors | When there is an error in the envelope creation process | 
{% /table %}

### Example Notifications

{% code %}
{% tab language="json" title="envelope_completion" %}
{
  "envelope_id": "<UUID>",
  "subscription_name": "envelope_completion"
  "status": "COMPLETE",
  "details": {
    "recipients": [
      {
        "id": "<UUID>",
        "sign_status": "SIGNED",
        "name": "User 1",
        "email": "example@yoti.com",
        "auth_type": "no-auth",
        "role": "just a role",
        "signed_at": "2021-01-01T00:00:00.000Z"
      }
    ],
    "completed_at": "2021-01-01T00:00:00.000Z",
    "files": [
      {
        "id": "<UUID>",
        "name": "sample.pdf"
      }
    ]
  }
}
{% /tab %}
{% tab language="json" title="upload_errors" %}
{
  "envelope_id": "<UUID>",
  "subscription_name": "upload_errors"
  "status": "ERRORED",
  "details": {
    "errors": [
      {
        "file_name": "sample.pdf",
        "code": "<ERROR MESSAGE>"
      }
    ]
  }
}
{% /tab %}
{% tab language="json" title="envelope_ready" %}
{
    "envelope_id": <UUID>,
    "subscription_name": "envelope_ready",
}
{% /tab %}
{% tab language="json" title="signer_completed" %}
{
    "envelope_id": "<UUID>",
    "subscription_name": "signer_completion"
    "status": "ACTIVE",
    "details":
    {
        "recipients":
        [
            {
                "id": "<UUID>",
                "sign_status": "SIGNED",
                "name": "User 1",
                "email": "example@yoti.com",
                "auth_type": "no-auth",
                "role": "just a role",
                "signed_at": "2021-01-01T00:00:00.000Z"
            }
        ],
        "completed_at": "2021-06-14T12:22:12.264Z",
        "files": [
        {
          "id": "<UUID>",
          "name": "sample.pdf"
        }
      ]
    }
}
{% /tab %}
{% /code %}