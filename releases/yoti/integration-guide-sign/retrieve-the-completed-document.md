---
type: page
title: Retrieve the completed document
listed: false
slug: retrieve-the-completed-document
description: 
index_title: Retrieve the completed document
hidden: 
keywords: 
tags: 
---

Once signed, a full copy of the completed document can be obtained by calling into the [Get Completed Document endpoint](https://yoti.com/api-reference/#yoti-sign-retrieve-the-completed-document). 

{% html %}
<div class="alert-GTK">
    <div class="alert-title" id="GTK">
        Good to know... 
    </div>
    <div class="alert-text">
       This returns PDFs and Word documents.
    </div>
</div>
{% /html %}

## Retrieve the completed document endpoint

Below is the end point used for get completed document.

{% code %}
{% tab language="http" %}
Sandbox GET https://demo.api.yotisign.com/v1/sign-requests/{sign_request_id}/completed-documents 
Production GET https://api.yotisign.com/v1/sign-requests/{sign_request_id}/completed-documents
{% /tab %}
{% /code %}

## Example

A complete example of how to [GET a completed document](https://yoti.com/api-reference/#yoti-sign-retrieve-the-completed-document) can be found below.

{% code %}
{% tab language="javascript" %}
const rp = require('request-promise');
const fs = require('fs');
const signRequestId = 'e2a78987-2c07-4b0a-96cf-b155ff6e60e9';
const options = {
    method: 'GET',
    uri: `${process.env.BASE_URL}/v1/sign-requests/${signRequestId}/completed-documents`,
    headers: {
        authorization: `Bearer ${process.env.API_KEY}`,
    },
    encoding: null
};
rp(options)
    .then(body => fs.writeFileSync('example.pdf', body)) // write pdf to file
    .catch(err => console.log(err.error));
{% /tab %}
{% /code %}

{% table %}
| Parameter | Description | 
| ---- | ---- | 
| Authorization\n\n\n\n(header) | Your API Key is required on all calls to the API and should be sent as a bearer token. | 
| Content-Type\n(header) | application/pdf | 
| sign_request_id\n\n(path) | This is a UUID referring to the Completed Document you are looking to retrieve. This will be the UUID obtained from the Create Sign Request endpoint | 
{% /table %}

On success, this endpoint returns a status code of 200 with the document as a PDF.

## Other response codes

{% table %}
| Response | Code | 
| ---- | ---- | 
| 401 | 401 is returned if a request is unauthorised. This is likely due to the API Key either being incorrect or not being sent properly in the headers. The key should be sent as a Bearer token over the authorisation header. | 
| 404 | If the requested document is not found you will receive a 404. This will be due to the request ID being invalid. | 
{% /table %}