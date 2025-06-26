---
type: page
title: Instructions
listed: true
slug: instructions
description: 
index_title: Instructions
hidden: 
keywords: 
tags: 
---

{% html %}
<div class="alert-BYS">
   <div class="alert-title" id="BYS">
      Before you start
   </div>
   <div class="alert-text">
      The Post Office LoDaS (Location and Data Services) API must be used to populate branch information. Not all branches offer the IBV service. <br/>
      To obtain the specification for this API, please contact <a href="mailto:clientsupport@yoti.com">clientsupport@yoti.com</a> stating your organisation name.
  </div>
</div>
{% /html %}

Here we will show you to generate instructions to send to the customer on:

- Applicant information
- List of documents
- Branch address
- Further information.
- A QR code that the person in branch will be required to scan.

{% code %}
{% tab language="http" %}
PUT https://api.yoti.com/idverify/v1/sessions/{sessionId}/instructions
{% /tab %}
{% /code %}

Once the requirement IDs have been retrieved for the ID and / or supplementary documents using the Fetch session endpoint, the instructions can be configured.

## Example

See below for a complete payload. This will just return a null body.

{% code %}
{% tab language="json" %}
{
  "contact_profile": {
    "first_name": "John",
    "last_name": "Doe",
    "email": "john.doe@gmail.com"
  },
  "documents": [
    {
      "requirement_id": "someIdDocumentRequirementId",
      "document": {
        "type": "ID_DOCUMENT",
        "country_code": "GBR",
        "document_type": "PASSPORT"
      }
    },
    {
      "requirement_id": "someSupplementaryDocumentRequirementId",
      "document": {
        "type": "SUPPLEMENTARY_DOCUMENT",
        "country_code": "GBR",
        "document_type": "UTILITY_BILL"
      }
    }
  ],
  "branch": {
    "type": "UK_POST_OFFICE",
    "name": "UK Post Office Branch",
    "address": "123 Post Office Road, London",
    "post_code": "ABC 123"
  }
}
{% /tab %}
{% /code %}

---

## Fetch instructions

This endpoint is used to pull the generated instructions PDF which you can send to the applicant. 

{% code %}
{% tab language="http" %}
GET https://api.yoti.com/idverify/v1/sessions/{sessionId}/instructions/pdf
{% /tab %}
{% /code %}

#### PDF Example

{% image url="https://uploads.developerhub.io/prod/kvAX/t91ck06tts3g3qs8zmd8b0glea6t18j1y824fg2lxlxt30lz43518apm6v8sbgul.png" mode="600" height="841" width="595" %}
{% /image %}