---
type: page
title: Knowledge base
listed: true
slug: knowledge-base-docscan
description: 
index_title: Knowledge base
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

**US Clients**

If you expect to receive US driving licences, state IDs, Canadian driving licences, or any document with a non-human-readable element on the rear of the document, we recommend that you set your manual_check configuration to 'ALWAYS' for security reasons.

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
| Endpoint | This is the endpoint that the integrating back-end can expose to Yoti, according to the notifications settings provided at session creation. Only HTTPS endpoints with TLS are supported.\n\n\nExposing this endpoint is not mandatory but highly recommended as it would avoid a continuous polling on the session retrieval endpoint. | 
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

---

## Document / Country selection

You can configure your Doc Scan session to add / remove which countries and document types are displayed to the user on the user view.

We provide 2 ways to customise countries or documents displayed:

1) **ORTHOGONAL_RESTRICTION**

Allows the user to WHITELIST or BLACKLIST by _country_ and _document type_ independently. If there is a WHITELIST for one country / document and a BLACKLIST for the other, then the BLACKLIST will overrule the WHITELIST.

{% code %}
{% tab language="json" %}
"filter": {
  "type": "ORTHOGONAL_RESTRICTIONS",
  "country_restriction": { // Optional
    "inclusion": "WHITELIST", // Required
    "country_codes": ["GBR", "FRA", "DEU"] // Required list
  },
  "type_restriction": { // Optional
    "inclusion": "BLACKLIST", // Required
    "document_types": ["NATIONAL_ID"] // Required list
  }
}
{% /tab %}
{% /code %}

{% image url="https://res.cloudinary.com/developerhub/image/upload/v1578930713/23602/vuiaacsoqcsbwn0qqaam.jpg" caption="Orthogonal restriction" mode="responsive" height="156" width="1036" %}
{% /image %}

**2) DOCUMENT_RESTRICTION**  - Allows the _Relying Business_ to provide multiple restrictions that filter by _country_ and _document type_ together. Multiple restrictions are combined and the _Union_ of all restrictions is used as either a WHITELIST or a BLACKLIST. This filter allows greater precision but is more verbose to use.

{% code %}
{% tab language="json" %}
"filter": {
  "type": "DOCUMENT_RESTRICTIONS",
  "inclusion": "BLACKLIST", // Required
  "documents": [ // Required
    {
      "country_codes": ["GBR","FRA"] // Optional
    },
    {
      "document_types": ["NATIONAL_ID","PASSPORT"] // Optional
    },
    {
      "country_codes": ["USA"], // Optional
      "document_types": ["DRIVING_LICENCE"] // Optional
    }
  ]
}
{% /tab %}
{% /code %}

{% image url="https://res.cloudinary.com/developerhub/image/upload/v1578930816/23602/u1czesnmeedv1p2jp5xi.jpg" caption="Document restriction" mode="responsive" height="166" width="1071" %}
{% /image %}

---

## Request multiple documents

It is possible to ask for more than one document from the user in one session.

{% html %}
<div class="alert-GTK">

    <div class="alert-title" id="GTK">

        Good to know

    </div>

    <div class="alert-text">

        If you are requesting multiple documents from your users you must make sure that you avoid creating sessions where the same document would be used to satisfy multiple selections.

    </div>

    <div class="alert-links"> 

   </div>

</div>
{% /html %}

To enable this use the required document array:

{% code %}
{% tab language="json" %}
"required_documents": [ // Optional
    {
      "type": "ID_DOCUMENT", // Required
      "filter": { // Optional
        "type": "ORTHOGONAL_RESTRICTIONS", // Required
        "country_restriction": { // Optional
          "inclusion": "WHITELIST", // Required
          "country_codes": ["GBR"] // Required
        },
        "type_restriction": { // Optional
          "inclusion": "BLACKLIST", // Required
          "document_types": ["NATIONAL_ID"] // Required
        }
      }
    },
    {
      "type": "ID_DOCUMENT",
      "filter": {
        "type": "DOCUMENT_RESTRICTIONS", // Required
        "inclusion": "BLACKLIST", // Required
        "documents": [ // Required
          {
            "country_codes": ["DEU","FRA"] // Optional
          },
          {
            "document_types": ["NATIONAL_ID","PASSPORT"] // Optional
          },
          {
            "country_codes": ["GBR"], // Optional
            "document_types": ["DRIVING_LICENCE"] // Optional
          }
        ]
      }
    }
  ],
{% /tab %}
{% /code %}

---

## Aadhaar

Yoti have launched supporting Aadhaar on Yoti Doc Scan!

The documents we support are:

- Aadhaar
- PAN
- Passport

Due to government restrictions Aadhaar numbers cannot be shared and it is mandatory to mask them. We return to businesses only masked images of Aadhaar. Unmasked images are deleted from our backend as soon as all checks are done. 

Example of masking of front and back of card:

{% image url="https://res.cloudinary.com/developerhub/image/upload/v1585254592/23602/kvkz5sfxemcuzst0djrp.jpg" caption="Aadhaar - Front" mode="300" height="772" width="1228" %}
{% /image %}

{% image url="https://res.cloudinary.com/developerhub/image/upload/v1585254605/23602/ourgxj9ze0zbe4mogr93.jpg" caption="Aadhaar - Back" mode="300" height="762" width="1198" %}
{% /image %}

There are many different formats for Aadhaar cards with the number possibly on the front and/or back. We will check both the back and the front of the card and mask any identified Aadhaar number. If there is no number detected then you will not be able to retrieve the images. The retrieval request will return 204 NO_CONTENT.

Aadhaar resources will only become available when the masking has been completed.