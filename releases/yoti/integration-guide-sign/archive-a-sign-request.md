---
type: page
title: Archive a sign request
listed: false
slug: archive-a-sign-request
description: 
index_title: Archive a sign request
hidden: 
keywords: 
tags: 
---

Sign Requests can be archived**.** The API exposes an [Archive Sign Request endpoint](https://yoti.com/api-reference/#yoti-sign-archive-a-sign-request) to achieve this:

## Archive a sign request endpoint

Below is the end point used for archive sign requests.

{% code %}
{% tab language="http" %}
Sandbox PATCH https://demo.api.yotisign.com/v1/sign-requests/{sign_request_id}
Production PATCH https://api.yotisign.com/v1/sign-requests/{sign_request_id}
{% /tab %}
{% /code %}

## Example

A complete example of how to [archive a sign request](https://yoti.com/api-reference/#yoti-sign-archive-a-sign-request) can be found below.

{% code %}
{% tab language="javascript" %}
const rp = require('request-promise');
const signRequestId = 'e2a78987-2c07-4b0a-96cf-b155ff6e60e9'; // id of document from Create Sign Request
const options = {
    method: 'PATCH',
    uri: `${process.env.BASE_URL}/v1/sign-requests/${signRequestId}`, // url of API
    headers: {
        authorization: `Bearer ${process.env.API_KEY}`, // API Key
    },
    body: {
        status: 'ARCHIVED',
    },
    json: true,
    resolveWithFullResponse: true,
};
rp(options)
    .then(response => {
        if (response.statusCode === 204) {
            // document cancelled
        }
    })
    .catch(err => console.log(err.error));
{% /tab %}
{% /code %}

{% table %}
| Parameter | Description | 
| ---- | ---- | 
| Authorization\n\n(header) | Your API Key is required on all calls to the API and should be sent as a bearer token. | 
| Content-Type\n(header) | application/json | 
| Body\n\n(body) | Archiving a Sign Request requires you to send a status of "ARCHIVED" in the body of your request\n\n`{``"status": "ARCHIVED"``}` | 
| sign_request_id (path) | This is a UUID referring to the Sign Request you are looking to archive. This will be the UUID obtained from the Create Sign Request endpoint | 
{% /table %}

The [Archive Sign Request endpoint](https://yoti.com/api-reference/#yoti-sign-archive-a-sign-request) returns a status code of 200 if successful.

## Other response codes

{% table %}
| Response | Description | 
| ---- | ---- | 
| 400 | The API returns a 400 if the parameter sent to it is incorrect. You may only send a status of 'ARCHIVED' or the request will be unsuccessful. | 
| 401 | 401 is returned if a request is unauthorised. This is likely due to the API Key either being incorrect or not being sent properly in the headers. The key should be sent as a Bearer token over the authorisation header. | 
| 404 | If the request is not found you will receive a 404. This will be due to the request ID being invalid. | 
{% /table %}