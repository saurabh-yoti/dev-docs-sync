---
type: page
title: Parent redirect object
listed: true
slug: parent-redirect-object
description: 
index_title: Parent redirect object
hidden: 
keywords: 
tags: 
---

On completion of the document being signed, you can specify a url for the signer to be redirected towards.

{% code %}
{% tab language="json" %}
"parent_redirect_urls":{
      "success":"https://someurl.com/success",
      "failure":"https://someurl.com/falure",
    }
{% /tab %}
{% /code %}

{% table %}
| Parameter | Description | 
| ---- | ---- | 
| success | The url the signer will be redirected towards on signing completion. Must be a valid url and the scheme must be HTTPS. | 
| failure | The url the signer will be redirected towards if an error occurs in the signing process. Must be a valid url and the scheme must be HTTPS. | 
{% /table %}