---
type: page
title: Create envelope
listed: true
slug: create-an-envelope-request
description: 
index_title: Create envelope
hidden: 
keywords: 
tags: 
---

An envelope serves as a container for all Yoti Sign transactions. When you create an envelope the following elements are configurable:

- File
- Name
- Email
- Reminders
- Envelope one time password
- Recipients including tags, auto-tagging and witnesses.
- Notifications
- Branding (only available with embedded flow)

Yoti offers two types of envelope flows:

1. [Yoti envelope](/eSignatures/yoti-envelope) - Yoti will handle the flow. 
2. [Embedded envelope ](/eSignatures/embedded-envelope)- The envelope will be rendered directly in the browser, commonly via an iFrame.

{% badge type="error" text="Important" /%} Authentication is important. Please ensure that any user signing through the embedded version are authenticated. You can do this by validating the email address or doing an IDV check on the user. More information is provided in the next section. 

---

## Headers explained

The following elements are needed in the header:

{% table %}
| Header | Description | 
| ---- | ---- | 
| Authorization | API Key to call the Yoti Sign API. This should be sent as a bearer token. | 
| Content-Type | multipart/form-data | 
{% /table %}

---

## Body explained

Each subpart should declare its appropriate **Content-Type:**

{% table %}
| Field | Description | 
| ---- | ---- | 
| file | Supported file types with content-type header with content-type header:\n\n\n- pdf (application/pdf)\n- .docx (application/vnd.openxmlformats-officedocument.wordprocessingml.template)\n- .doc (application/msword) | 
| options | application/json | 
{% /table %}

There must be at least 1 file and a maximum of 20. When sending multiple documents, they will be received in the order sent.

{% badge type="success" text="Hint" /%} If you have access to the Yoti Sign portal you can retrieve a template with example JSON. See [Templates](/yoti-developer-documentation/v6.0/eSignatures/templates).