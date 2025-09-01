---
type: page
title: Retrieve images
listed: true
slug: retrieve-image
description: 
index_title: Retrieve images
hidden: 
keywords: 
tags: 
---

In order to retrieve document images from the **resources** container we'll want to look for the relevant media ID inside of the id document pages.

For security reasons, Yoti does not include personally identifiable information within the standard response to a session retrieval request. Yoti will provide ID's to media associated with the session, which can be stored and retrieved separately.

{% code %}
{% tab language="javascript" title="Node.js" %}
idvClient.getMediaContent(sessionId, pageMediaId).then(media => {
    const buffer = media.getContent();
    const base64Content = media.getBase64Content();
    const mimeType = media.getMimeType();
    // handle base64content or buffer
}).catch(error => {
    console.log(error)
    // handle error
})
{% /tab %}
{% tab language="java" %}
Media media = docScanClient.getMediaContent(sessionId, pageMediaId);
{% /tab %}
{% tab language="php" %}
<?php
$media = $docScanClient->getMediaContent($sessionId, $pageMediaId);
$base64Content = $media->getBase64Content();
$contentType = $media->getMimeType();
{% /tab %}
{% tab language="python" %}
media = doc_scan_client.get_media_content(session_id, pageMediaId)
base64_content = media.base64_content
content_type = media.mime_type
{% /tab %}
{% tab language="csharp" %}
MediaValue media = docScanClient.GetMediaContent(sessionId, pageMediaId);
{% /tab %}
{% /code %}

### Retrieve document id photo

In order to retrieve specific portrait ID document image from the resources container we'll want to look for the relevant media ID inside of the id document container. 

{% code %}
{% tab language="javascript" title="Node.js" %}
idvClient.getMediaContent(sessionId, documentPhotoId).then(media => {
    const buffer = media.getContent();
    const base64Content = media.getBase64Content();
    const mimeType = media.getMimeType();
    // handle base64content or buffer
}).catch(error => {
    console.log(error)
    // handle error
})
{% /tab %}
{% tab language="java" %}
Media media = docScanClient.getMediaContent(sessionId, documentPhotoId);
{% /tab %}
{% tab language="php" %}
<?php
$media = $docScanClient->getMediaContent($sessionId, $documentPhotoId);
$base64Content = $media->getBase64Content();
$contentType = $media->getMimeType();
{% /tab %}
{% tab language="python" %}
media = doc_scan_client.get_media_content(session_id, documentPhotoId)
base64_content = media.base64_content
content_type = media.mime_type
{% /tab %}
{% tab language="csharp" %}
MediaValue media = docScanClient.GetMediaContent(sessionId, documentPhotoId);
{% /tab %}
{% /code %}