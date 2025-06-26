---
type: page
title: Delete session
listed: true
slug: delete-session
description: 
index_title: Delete session
hidden: 
keywords: 
tags: 
---

It is possible to delete a session or image (media) before the defined retention period (ttl) is over.

Deleting the session will also delete all media from that session.  You can delete a session yourself by sending a DELETE request to the endpoint below.

{% code %}
{% tab language="http" %}
DELETE https://api.yoti.com/idverify/v1/sessions/{sessionId}
{% /tab %}
{% /code %}

Yoti recommends starting a new session for the same applicant doing a re-verification or needing to edit their session.

The following endpoint allows deletion of a specific media object, without deleting the entire session.

{% code %}
{% tab language="http" %}
DELETE https://api.yoti.com/idverify/v1/sessions/{sessionId}/media/{mediaId}/content
{% /tab %}
{% /code %}