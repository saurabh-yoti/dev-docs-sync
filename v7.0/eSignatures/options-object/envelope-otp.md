---
type: page
title: Envelope OTP
listed: true
slug: envelope-otp
description: 
index_title: Envelope OTP
hidden: 
keywords: 
tags: 
---

If you would like to enable an SMS two factor authentication you can enable this in your request.

If you have this as true you will need to know the following:

- A mobile number for the signer so we can send them a one-time password when their document is ready to be signed.
- ISO country code.

Please see recipient section for more details.

{% code %}
{% tab language="json" %}
{ "has_envelope_otps": true,}
{% /tab %}
{% /code %}

{% table %}
| Parameter | Description | 
| ---- | ---- | 
| has_envelope_otp | Boolean, to determine if the envelope access requires OTP verification\n\n\n\n- TRUE\n- FALSE | 
{% /table %}