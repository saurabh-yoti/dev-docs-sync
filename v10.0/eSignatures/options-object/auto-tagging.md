---
type: page
title: Auto-tagging
listed: true
slug: auto-tagging
description: 
index_title: Auto-tagging
hidden: 
keywords: 
tags: 
---

Auto-tagging is an **optional** property and is used to automatically place fields in documents which have been set up for Auto-tagging. This is an extension of templates.

Yoti has created three matrix's. 

{% table %}
| Name | Matrix | 
| ---- | ---- | 
| GENERAL | [General matrix](https://www.yoti.com/wp-content/uploads/Sign_Auto-tagging-matrix.pdf) | 
| REAL_ESTATE | [Real estate matrix](https://www.yoti.com/wp-content/uploads/Sign_real-estate-autotagging-matrix.pdf) | 
| ALL | This will search through all the matrix's listed above. | 
{% /table %}

{% code %}
{% tab language="json" %}
{
  "autotagging": "GENERAL",
}
{% /tab %}
{% /code %}

For more information head over to our [auto-tagging recipient](/eSignatures/auto-tagging--recipient-) section.