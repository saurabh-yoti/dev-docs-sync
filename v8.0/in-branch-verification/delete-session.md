---
type: page
title: Delete Session
listed: true
slug: delete-session
description: 
index_title: Delete Session
hidden: 
keywords: 
tags: 
---

It is possible to delete a session or image (media) before the defined retention period (ttl) is over.

Deleting the session will also delete all media from that session. You can delete a session yourself by sending a DELETE request to the endpoint below.

{% code %}
{% tab language="http" %}
DELETE https://api.yoti.com/idverify/v1/sessions/{sessionId}
{% /tab %}
{% /code %}

SDK Example:

{% code %}
{% tab language="javascript" %}
const { RequestBuilder} = require("yoti");

const request = new RequestBuilder()
  .withBaseUrl("https://api.yoti.com/idverify/v1")
  .withPemFilePath("<YOTI_KEY_FILE_PATH>") // file path to PEM file
  .withEndpoint("/sessions/<sessionId>")
  .withMethod("DELETE")
  .withQueryParam("sdkId", "<YOTI_CLIENT_SDK_ID>")
  .build();

//get Yoti response
const response = await request.execute();
{% /tab %}
{% /code %}

Yoti recommends starting a new session for the same applicant doing a re-verification or needing to edit their session.