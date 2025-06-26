---
type: page
title: Authentication and headers
listed: true
slug: authentication-and-headers
description: 
index_title: Authentication and headers
hidden: 
keywords: 
tags: 
---

All requests to a Yoti API require a form of authentication. This API requires the following headers:

{% table %}
| Header | Description | Example | 
| ---- | ---- | ---- | 
| X-Yoti-Auth-Digest | Base64 encoded signed hash of the request, signed using the Key file\n\npair associated with your Yoti Application. Steps to generate are described\n\nbelow&lt;br&gt; | &lt;p&gt;qoMA1Pb8IaC4vv7DzgkZY5tD0hkHT&lt;span&gt;bV1rnFX3EDMfr3lHilbdZakE......&lt;/span&gt;&lt;/p&gt; | 
| X-Yoti-Auth-Id | The SDK ID associated with the Yoti Application.&lt;br&gt; | b3c6bed3-8f17-46b1-a008-3aebc2da0b79 | 
{% /table %}

The X-Yoti-Auth-Digest should be a concatenation of the following:

- HTTP method, e.g. POST
- URI Path, e.g. /sessions/ (always exclude /idverify/v1 when signing)
- The query string (complete with the timestamp and nonce parameters)
- Base64 encoded value of the JSON payload

These should be joined with an ‘&’. For example:

{% table %}
| Examples | 
| ---- | 
| POST&amp;/sessions?sdkId={sdkId}&amp;nonce=24487c75-0d20-457f-918a-c0abe5b1473b&amp;timestamp=1541694094210&amp;qojdsdgGDGb8IaC......&lt;br&gt; | 
| GET&amp;/sessions/{session_id}?sdkId={sdkId}&amp;nonce=24487c75-0d20-457f-918a-c0abe5b1473b&amp;timestamp=1541694094210 | 
{% /table %}

The above concatenated string should then be signed using the Yoti Application PEM file, and the resulting signature encoded in Base64.

Timestamps are Unix timestamps.

Nonces are UUID strings.