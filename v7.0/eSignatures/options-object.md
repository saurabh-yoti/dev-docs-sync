---
type: page
title: Options object
listed: true
slug: options-object
description: 
index_title: Options object
hidden: 
keywords: 
tags: 
---

There are four property types:

- Name
- Email
- Reminders
- Envelope OTP

---

## Name property

This is the name of the envelope. It will be presented as the email subject and the document tag in the email.

{% code %}
{% tab language="json" %}
{
    "name": "envelope name",
}
{% /tab %}
{% /code %}

{% table %}
| Parameter | Description | 
| ---- | ---- | 
| name | This must be between 1 and 65 characters and must not contain special characters: `/:*?<>&#124;` | 
{% /table %}

---

## Email property

This service will send an email to the recipient prompting them through the Yoti Sign flow. There is a configurable option to customise the signing request message that gets sent. 

The API will require an invitation object and message. This message will be included within the email sent to your recipients.

{% code %}
{% tab language="json" %}
{
    "emails": {
        "invitation": {
            "body": {
                "message": "Please sign this document"
            }
        },

    },
}
{% /tab %}
{% /code %}

{% image url="https://res.cloudinary.com/developerhub/image/upload/v1616004720/v2_2762/pplgz6bqznglccaqlscz.png" caption="Body &gt; Email object" mode="600" height="542" width="614" %}
{% /image %}

{% table %}
| Parameter | Description | 
| ---- | ---- | 
| email | The email parameter lets you specify a message to be sent to a recipient. See example above. | 
| message | The message that appears the bottom of the email or template with instructions for the user. This must be between 1 and 600 characters. | 
{% /table %}

{% badge type="info" text="Hint" /%} Typically through embedded signing emails may not be required, as the flow is intended to be solely within the browser.

{% badge type="error" text="Important" /%} Invitation is **not** required to be present **IF** the `signer_invitation` is not present in the `event_notifications` array.