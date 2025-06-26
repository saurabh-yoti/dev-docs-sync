---
type: page
title: Optional attributes
listed: false
slug: optional-attributes
description: 
index_title: Optional attributes
hidden: 
keywords: 
tags: 
---

If you do not require an attribute as a mandatory request, you can mark an attribute as optional. To enable this feature please follow the instructions below:

1. Log on to the [**Yoti Hub**](https://hub.yoti.com/login)
2. Head over to your application and scenario. 
3. Go to the bottom and you will see advanced settings:

{% image url="https://uploads.developerhub.io/prod/kvAX/1jivz1bo0rmltsf2p3oip15qv7100lnj2svfg7l6m6894x1w5lkszooie79qovbd.png" caption="Application &gt; Scenario &gt; Advanced settings" mode="300" height="1070" width="940" %}
{% /image %}

4. Click advanced policy editor.
5. Add true / false to the optional field. 

{% code %}
{% tab language="json" %}
{
name: 'date_of_birth', 
anchors: [], 
derivation: '', 
optional: true,
accept_self_asserted: false, 
alternative_names: [] 

},
{% /tab %}
{% /code %}

{% badge type="info" text="Hint" /%} Attributes that can request from users using the advanced view are: document_details and document_images.