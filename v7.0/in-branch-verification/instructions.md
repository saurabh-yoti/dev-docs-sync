---
type: page
title: Instructions
listed: false
slug: instructions
description: 
index_title: Instructions
hidden: 
keywords: 
tags: 
---

Here we will show you to generate instructions to send to the customer on:

- Applicant information
- List of documents
- Branch address
- Further information.
- A QR code that the person in branch will be required to scan.

{% code %}
{% tab language="http" %}
PUT /sessions/{sessionId}/instructions
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
    "fad_code": 1234567,
    "name": "UK Post Office Branch",
    "address": "123 Post Office Road, London",
    "post_code": "ABC 123",
    "location": {
      "latitude": 0.34322,
      "longitude": -42.48372
    }
  }
}
{% /tab %}
{% /code %}

---

## Fetch instructions

This endpoint is used to pull the generated instructions PDF which you can send to the applicant. 

{% code %}
{% tab language="http" %}
GET https://api.yoti.com/sessions/{sessionId}/instructions/pdf
{% /tab %}
{% /code %}