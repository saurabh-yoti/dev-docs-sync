---
type: page
title: Knowledge base Dev
listed: true
slug: knowledge-base-docscan
description: 
index_title: Knowledge base Dev
hidden: 
keywords: 
tags: 
---

This is your online library of information about Yoti Doc Scan.

## FAQs

Some of our most asked questions from integrators and businesses.

**[View Developer FAQs](https://yoti.zendesk.com/hc/en-us/sections/360001353077-Yoti-Doc-Scan)**

---

## ID Document Text Data extraction explained

There are two methods of extracting structured data from documents:

- Machine data extraction, using a suitable extraction method for that document type.
- Manual review and data entry

Machine data extraction will always be used in place of human data entry if possible for that document type. Generally there are two main reasons machine data extraction is not successful:

1) The images used as an input are not of a high enough quality.

2) There are no available machine extraction methods for the document type submitted. For more information on the documents where machine data extraction is available, ​please [contact us](mailto:sdksupport@yoti.com).​

US Clients

If you expect US driving licences, state IDs, Canadian driving licences, or any document with a non-human-readable element on the rear of the document, we recommend that you set your manual_check configuration to 'ALWAYS' for security reasons."

---

## Notifications

Every time the session state changes, based on the selected subscription topics you can request a notification on progress.

{% code %}
{% tab language="json" %}
// Optional
  "notifications": {
    // Yoti Docs posts (POST endpoint required) an update notification to this endpoint
    // every time the session state changes based on the selected subscription topics
    // (resource_update, check_completion, task_completion. etc.)
    "endpoint": "https://yourdomain.com/idverify/updates",
    "topics": [
      "resource_update",
      "task_completion",
      "check_completion",
      "session_completion"
    ],
    // Optional. If provided, Yoti will send this as a base64 encoded value for the
    // Authorization header in the notifications that are sent to your endpoint
    "auth_token": "username:password"

  },
{% /tab %}
{% /code %}

Optionally, it is possible to specify a Webhook URL when creating a Yoti Doc Scan request to be informed of any changes that occur within the session. This avoids the need to poll for updates. Here is an example object that can get provided to the Doc Scan API which specifies a notifications endpoint, and a list of topics to be subscribed to.

{% table %}
| Component | Description | 
| ---- | ---- | 
| Endpoint | This is the endpoint that the integrating back-end can expose to Yoti, according to the notifications settings provided at session creation.\n\n\nExposing this endpoint is not mandatory but highly recommended as it would avoid a continuous polling on the session retrieval endpoint. | 
| Topics | Resource_update - update received whenever there are changes to **resources** in the Yoti Doc Scan session. For example, a user uploading a new document.\n\n\nTask_completion - A task completion event is triggered whenever a selected task has been completed. If you require TEXT_EXTRACTION and the check has been fulfilled, Yoti will send this through as an update to your endpoint.\n\n\nCheck_completion - Similarly to task_completion, a check completion event is triggered when a selected check has been completed, for example a document authenticity check being performed.\n\n\nSession_completion - Triggered when all tasks and all checks inside of a given session have been completed.\n\n\nauth_token - We recommend protecting any exposed routes with basic authorisation. You may specify a basic auth token to the Yoti Doc Scan API to be used when sending notifications to your endpoint. Credentials are automatically converted to base64 and sent in the Authorisation header. For example "auth_token": "username:password" would result in Authorization: Basic dXNlcm5hbWU6cGFzc3dvcmQ= being sent into the request header from Yoti. | 
{% /table %}

### Example response

{% code %}
{% tab language="json" %}
{
    // Always provided
    "session_id" : "<uuid>",
    "topic" : "resource_update", // | "task_completion" | "check_completion" | "session_completion"
    // Optional and present only when "topic" is "task_completion"
    "task_id" : "<uuid>",
    // Optional and present only when "topic" is "resource_update"
    "resource_id" : "<uuid>",
    // Optional and present only when "topic" is "check_completion"
    "check_id" : "<uuid>"
  }
{% /tab %}
{% /code %}