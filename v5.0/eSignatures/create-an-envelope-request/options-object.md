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

There are two property types:

- Name
- Email

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
| name | This must be between 1 and 65 characters | 
{% /table %}

## Email property

This service will send an email to the recipient prompting them through the Yoti Sign flow. There is a configurable option to customise the signing request message that gets sent. The API will require an invitation object and message. This message will be included within the email sent to your recipients.

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
| message | The message that appears the bottom of the email or template with instructions for the user. This must be between 1 and 600 characters | 
{% /table %}

## Reminder property

You can configure reminders to be sent to recipients who still have active documents that need signing. There will be 3 reminders (this is not currently configurable).

{% code %}
{% tab language="json" %}
{
      "reminders": {
          "frequency": 1
      },
}
{% /tab %}
{% /code %}

{% table %}
| Parameter | Description | 
| ---- | ---- | 
| Frequency | Needs to be of value 0, 1, 2 or 7 | 
{% /table %}

## Envelope OTP

{% code %}
{% tab language="json" %}
{
  "has_envelope_otps": true,
}
{% /tab %}
{% /code %}

{% table %}
| Parameter | Description | 
| ---- | ---- | 
| has_envelope_otp | Boolean, to determine if the envelope access requires OTP verification\n\n\n\n- TRUE\n- FALSE | 
{% /table %}