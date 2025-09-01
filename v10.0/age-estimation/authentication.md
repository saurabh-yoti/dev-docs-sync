---
type: page
title: Authentication
listed: true
slug: authentication
description: 
index_title: Authentication
hidden: 
keywords: 
tags: 
---

{% callout type="warning" title="Warning" %}
This step requires API keys.

To generate your keys, please refer to [auto$](/age-estimation/production-keys)
{% /callout %}

From here on, each endpoint requires an RSA-signed request for Authentication. This can either be constructed manually or via one of our backend SDKs. The Yoti SDK exposes a simple request builder class to support the authentication process, and the examples provide snippets of this usage which should be applied to each endpoint. You will need your Yoti SDK ID and application key pair for either process.

The method is detailed below if you prefer to authenticate without the SDK.

The Base URL for requests is: [https://api.yoti.com/ai/v1](https://api.yoti.com/ai/v1)

The endpoints are listed in the relevant documentation, depending on the service. e.g. /age-antispoofing

{% callout type="info" title="Info" %}
If using the Yoti SDK, you may skip the below and continue to the next pages for code snippet examples
{% /callout %}

## Generate signed request

Yoti API endpoints are authenticated through signed requests, and the current approach for building signed requests consists of passing the following HTTP Headers

{% table %}
| Header Name | Header Value | 
| ---- | ---- | 
| X-Yoti-Auth-Digest | The signed digest of the request, computed through the below instructions | 
| X-Yoti-Auth-Id | The SDK ID generated via the Hub | 
{% /table %}

Here's how to compute it:

1. Concatenate the HTTP method, the path, the query string (enriched with a timestamp and a nonce parameter) and the base64 encoded request body, if available, using the & character.

Example GET request:

{% code %}
{% tab language="http" %}
GET GET&{endpoint}?nonce=b88ad843-13cc-44ba-a3e0-053f71d89b1f&timestamp=1480509893
{% /tab %}
{% /code %}

Example POST request:

{% code %}
{% tab language="http" %}
POST POST&{endpoint}?nonce=b88ad843-13cc-44ba-a3e0-053f71d89b1f&timestamp=1480509893&ew0KImlkIiA6IDEsDQoibmFtZSIgOiBpdGVtDQoNCn0=
{% /tab %}
{% /code %}

2. Apply SHA256withRSA to the string generated from step 1, using your PEM private key generated from the Yoti Hub.
3. Base64 encode the result from 2, so that it can be sent as a string header.

{% table %}
| Parameter | Description | 
| ---- | ---- | 
| nonce | UUID V4 | 
| timestamp | Current UNIX timestamp | 
{% /table %}