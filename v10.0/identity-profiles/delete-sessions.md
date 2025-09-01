---
type: page
title: Delete Sessions
listed: true
slug: delete-sessions
description: 
index_title: Delete Sessions
hidden: 
keywords: 
tags: 
---


It is possible to delete a session or image (media) before the defined [retention period (ttl)](https://developers.yoti.com/identity-verification/system-preferences) is over. This can only be done **once the session is completed.**

Deleting the session will also delete all media from that session. Deleting a media object will delete only that specific object, leaving the rest of the session untouched.


{% code %}
{% tab language="javascript" %}
// Deleting the session
idvClient.deleteSession(sessionId).then(() => {
  // Session has been deleted
}).catch(error => {
  // Error occured
})

// Deleting the media
idvClient.deleteMediaContent(sessionId, mediaId).then(() => {
  // Media has been deleted
}).catch(error => {
  // Error occured
})
{% /tab %}
{% tab language="java" %}
// Deleting the session
docScanClient.deleteSession(sessionId);

// Deleting the media
docScanClient.deleteMediaContent(sessionId, mediaId);
{% /tab %}
{% tab language="php" %}
<?php
// Deleting the session
$docScanClient->deleteSession($sessionId);

// Deleting the media
$docScanClient->deleteMediaContent($sessionId, $mediaId);
{% /tab %}
{% tab language="python" %}
# Deleting the session
doc_scan_client->delete_session(session_id);

# Deleting the media
doc_scan_client->delete_media_content(session_id, media_id);
{% /tab %}
{% tab language="csharp" %}
// Deleting the session
docScanClient.DeleteSession(sessionId);

// Deleting the media
docScanClient.DeleteMediaContent(sessionId, mediaId);
{% /tab %}
{% /code %}


