---
type: page
title: Reminders
listed: true
slug: Reminders
description: 
index_title: Reminders
hidden: 
keywords: 
tags: 
---

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