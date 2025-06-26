---
type: page
title: Status of sign request Dev
listed: true
slug: status-of-sign-request
description: 
index_title: Status of sign request Dev
hidden: 
keywords: 
tags: 
---

Checking the status of a Sign Request is achieved through the [GET sign request endpoint.](https://yoti.com/api-reference/#yoti-sign-status-of-sign-request)

## Status of sign request endpoint

Below is the end point used for get sign request.

{% code %}
{% tab language="http" %}
Sandbox GET https://demo.api.yotisign.com/sign-requests/{sign_request_id}
Production GET https://api.yotisign.com/sign-requests/{sign_request_id}
{% /tab %}
{% /code %}

## Example

A complete example of how to [GET the status of a sign request](https://yoti.com/api-reference/#yoti-sign-status-of-sign-request) can be found below.

{% code %}
{% tab language="javascript" %}
const rp = require('request-promise');
const signRequestId = 'e2a78987-2c07-4b0a-96cf-b155ff6e60e9';
const options = {
    method: 'GET',
    uri: `${process.env.BASE_URL}/v1/sign-requests/${signRequestId}`,
    headers: {
        authorization: `Bearer ${process.env.API_KEY}`,
    },
};
rp(options)
    .then(body => {
        // returns specified sign request
    })
    .catch(err => console.log(err.error));
{% /tab %}
{% /code %}

{% table %}
| Parameter | Description | 
| ---- | ---- | 
| Authorization\n\n(header) | Your API Key is required on all calls to the API and should be sent as a bearer token. | 
| Content-Type\n(header) | application/json | 
| sign_request_id\n\n\n\n(path) | This is a UUID referring to the Sign Request you are looking to retrieve. This will be the UUID obtained from the Create Sign Request endpoint | 
{% /table %}

## Example of response

On success, we return a 200 with a JSON body matching the following schema.

{% code %}
{% tab language="json" %}
{
  "id": "3fa85f64-5717-4562-b3fc-2c963f66afa6",
  "completed_at": "2019-07-11T09:16:11.205Z",
  "status": "COMPLETE",
  "file_name": "string",
  "completed_file_location": "https://yotisign.com/api/v1/sign_requests/{sign_request_id}/completed-documents",
  "recipients": [
    {
      "id": "3fa85f64-5717-4562-b3fc-2c963f66afa6",
      "sign_status": "SIGNED",
      "role": "string",
      "signed_at": "2019-07-11T09:16:11.205Z",
      "name": "string",
      "email": "user@example.com",
      "yoti_attributes": [
        "postal_address"
      ]
    }
  ]
}
{% /tab %}
{% /code %}

{% table %}
| Response | Description | 
| ---- | ---- | 
| id | The sign request ID, this identifies the sign request. | 
| completed_at | Once all signees have signed the document it is marked as COMPLETE, the completed_at field stores the timestamp of when the last signee completes the request. | 
| status | The status of a sign request can either be "COMPLETE", "ACTIVE" or "ARCHIVED. A sign request defaults to "ACTIVE" and will remain in this state until all signees have signed the document. Once it is fully signed the state will update to "COMPLETE". A status may be "ARCHIVED" if you archive a document using the archive sign request endpoint. | 
| file_name | The name of the document as specified in the create sign request body. | 
| completed_file_location | This is the location of the completed document, this URL may be used with valid authentication to retrieve the completed document at a later date. | 
| recipients | An array containing the list of signees and a breakdown of their status in regards to the sign request. | 
{% /table %}

{% table %}
| Response (Recipients) | Description | 
| ---- | ---- | 
| id | Used to identify who has signed this document. | 
| sign_status | The sign_status may be one of either "SIGNED" or "UNSIGNED" | 
| role | The role is returned as specified when creating the sign request. | 
| signed_at | A timestamp indicating when the signee signed the document. | 
| name | The name of the signee | 
| email | The email address of the signee. | 
| yoti_attributes | If the sign request was sent to a signee requesting yoti_attributes, the list of signed attributes are returned, this an array of any of the following values \n\n[postal address, selfie, full_name, date_of_birth, gender, nationality, phone_number]. | 
{% /table %}

## Other response codes

{% table %}
| Response | Description | 
| ---- | ---- | 
| 401 | 401 is returned if a request is unauthorised. This is likely due to the API Key either being incorrect or not being sent properly in the headers. The key should be sent as a Bearer token over the authorisation header. | 
| 404 | If the request is not found you will receive a 404. This will be due to the request ID being invalid. | 
{% /table %}