---
type: page
title: Send your own instructions
listed: false
slug: send-your-own-instructions
description: 
index_title: Send your own instructions
hidden: 
keywords: 
tags: 
---

This section will explain how to retrieve the PDF of instructions and send to the end user. You can ignore this section if you do not use the notification INSTRUCTIONS_EMAIL_REQUESTED.

## Get contact information

{% code %}
{% tab language="http" %}
GET https://api.yoti.com/sessions/<sessionId>/instructions/contact-profile
{% /tab %}
{% /code %}

If you only want the contact information to send the PDF too you will need to use the below GET endpoint.

### Example response

{% code %}
{% tab language="json" %}
"contact_profile": { 
    "first_name": "someFirstName",
    "last_name": "someFirstName", 
    "email": "someFirstName", 
  }
{% /tab %}
{% /code %}

---

## Get instructions

Sending the GET request below will return details about the required documents and the address of the post office branch that will be used by the user that is linked to the sessionId.

{% code %}
{% tab language="http" %}
GET https://api.yoti.com/sessions/<sessionId>/instructions
{% /tab %}
{% /code %}

### Example response

{% code %}
{% tab language="json" %}
{
  "contact_profile": { 
    "first_name": "someFirstName", 
    "last_name": "someFirstName", 
    "email": "someFirstName", 
  },
  "documents": [ 
    {
      "requirement_id": "abc123", 
      "document": {
        "type": "ID_DOCUMENT", // ID_DOCUMENT or SUPPLEMENTARY_DOCUMENT
        "country_code": "GBR",
        "document_type": "PASSPORT" 
      }
    },
    {
      "requirement_id": "def789",
      "document": {
        "type": "SUPPLEMENTARY_DOCUMENT",
        "country_code": "GBR",
        "document_type": "UTILTIY_BILL"
      }
    }
  ],
  "branch": { 
    "type": "UK_POST_OFFICE",
    "fad_code": "3108015", 
    "name": "Stonehaven", 
    "address": "Ellon Stall Supermarket, 48 Allardice Street, Stonehaven, Aberdeenshire", 
    "post_code": "AB39 2BU",
    "location": {
      "latitude": "56.96438",
      "longitude": "-2.2079"
  }
}
{% /tab %}
{% /code %}

## Get the PDF

Yoti will generate a PDF, you can use the following GET endpoint to retrieve this PDF.

{% code %}
{% tab language="http" %}
GET https://api.yoti.com/sessions/<sessionId>/instructions/pdf
{% /tab %}
{% /code %}