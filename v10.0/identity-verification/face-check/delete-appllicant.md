---
type: page
title: Delete applicant data
listed: true
slug: delete-appllicant
description: 
index_title: Delete applicant data
hidden: 
keywords: 
tags: 
---

You can delete all information about the applicants or applicant pools at any time using our API endpoints. Integrators can use our sdk request builders to make the calls to our API endpoints. On successful requests a 204 response code will be sent.

{% code %}
{% tab language="javascript" title="Node.js" %}
const { RequestBuilder, Payload } = require("yoti");

const request = new RequestBuilder()
  .withBaseUrl("https://api.yoti.com/idverify/v1")
  .withPemFilePath("<YOTI_KEY_FILE_PATH>") // file path to PEM file
  .withEndpoint("/applicants/<applicant_id>")
  .withMethod("DELETE")
  .withQueryParam("sdkId", "<YOTI_CLIENT_SDK_ID>")
  .build();

// get Yoti response
const response = await request.execute();
{% /tab %}
{% /code %}

---

## Delete applicant

Call the below endpoint to delete the image of the face from an applicant:

{% code %}
{% tab language="http" %}
DELETE https://api.yoti.com/idverify/v1/applicants/<applicant_id>
{% /tab %}
{% /code %}

---

## Delete face

Call the below endpoint to delete the image of the face from an applicant:

{% code %}
{% tab language="http" %}
DELETE https://api.yoti.com/idverify/v1/applicants/<applicant_id>/faces/<face_id>
{% /tab %}
{% /code %}

---

## Delete applicant pool

Call the below endpoint to delete an applicant pool:

{% code %}
{% tab language="http" %}
DELETE https://api.yoti.com/idverify/v1/pools/<pool_id>
{% /tab %}
{% /code %}

---

## Delete applicant from pool

Call the below endpoint to delete an applicant from a specific applicant pool:

{% code %}
{% tab language="http" %}
DELETE https://api.yoti.com/idverify/v1/pools/<pool_id>/applicants/<applicant_id>
{% /tab %}
{% /code %}