---
type: page
title: Overview
listed: true
slug: overview
description: 
index_title: Overview
hidden: 
keywords: 
tags: 
---

Across Yoti's suite of services, we have numerous APIs that you can use to perform checks

All API calls will be made using an OAuth Access Token as a bearer token. 

The required steps to generate this Access Token and make API calls to Yoti are as follows:

1. Generate a JWT token using a Yoti private key (.pem file)
2. Acquire an OAuth Access Token using this JWT Token
3. Send an API request to Yoti

{% cards view="grid" %}
{% card title="Generate a JWT Token" link="/central-authentication/generate-a-jwt-token" %}
This will be used to request an OAuth token from our authentication service
{% /card %}
{% card title="Generate an OAuth Token" link="/central-authentication/generate-an-oauth-token" %}
This will be used to authenticate your API calls to Yoti
{% /card %}
{% card title="Send your API request" link="/central-authentication/send-an-api-request" %}
Use a Yoti API to complete checks on your users
{% /card %}
{% /cards %}

An OAuth token can be reused for multiple requests - you must **NOT** use a new token for every request. There is a limit of 200 active tokens per application/SDK ID. We advise that you use one key for all calls within a scope and obtain a new token every 30 minutes. 

{% callout type="warning" title="Before you start" %}
You will need to set up your organisation within the Yoti Hub, and we will need to verify this organisation account before you can generate a .pem file 

[Create an Organisation](/central-authentication/getting-started)
{% /callout %}

### Limitations

We will enforce a limit on the maximum number of active API tokens for a given application / SDK ID. The limit is 200 active tokens.

Tokens issued are valid for a fixed 45 minute period. A new token should be obtained every 30 minutes which will give you plenty of leeway to retry if the operation fails