---
type: page
title: Yoti Sign API Integration
listed: true
slug: yoti-sign-api-integration
description: 
index_title: Yoti Sign API Integration
hidden: 
keywords: 
tags: 
---

Yoti Sign offers the convenience and simplicity of e-signing platforms, but with the optional added security of biometric verification providing immutable proof of the signees identity. 

This document will guide you through the configuration and implementation steps that are necessary in order for your back-end to be able to retrieve and send PDF's for users to electronically sign.

The integration process involves five simple steps:

1) [Company onboarding](/yoti-sign/yoti-sign-api-integration#step-1-onboarding)

The Yoti Sign API gives you programatic access to perform the following actions:

2) [Create a Sign Request](/yoti-sign/yoti-sign-api-integration#step-2-creating-a-sign-request) 

3) [Archive a Sign Request](/yoti-sign/yoti-sign-api-integration#step-3-archive-a-sign-request)

4) [Get a Sign Request](/yoti-sign/yoti-sign-api-integration#step-4-get-a-sign-request)

5) [Get a Completed Document](/yoti-sign/yoti-sign-api-integration#step-5-get-a-completed-document)

---

## Support

If you have any questions regarding this API please do not hesitate to contact [sdksupport@yoti.com](mailto:sdksupport@yoti.com).

Once we have answered your question we may contact you again to discuss Yoti products and services. If you’d prefer us not to do this, please let us know when you e-mail.

---

## Technical Flow

There are two types of users in the Yoti Sign flow:

The Sender - This user will be sending out the PDF and requesting a signed document back.

The Signee - This user will be receiving the PDF and sending the digitally signed document to the sender.

Both roles are technically explained below:

### Sender

A user makes a call to the Yoti Sign sign_request endpoint with the appropriate data (detailed in the integration steps below). This data contains information about the signee of the document, and where the signee should sign on the page.

{% image url="https://image-archive.developerhub.io/image/upload/17288/w5wlchnlj8tvw0oihf25/1564055966.png" mode="responsive" height="1200" width="1600" %}
{% /image %}

### Signee

A user clicks on an email and is taken through the usual Yoti Sign flow and once complete, a post message is sent to the webhook URI with the URL of the completed document.

{% image url="https://image-archive.developerhub.io/image/upload/17288/enwm0wfiznlqvzcw6wg5/1564056013.png" mode="responsive" height="1200" width="1600" %}
{% /image %}

---

## Step 1: Onboarding

Before you begin, you will need to register to use Yoti Sign. To register, fill out [this](https://www.yotisign.com/app/contact-us/) form to receive your free 30 day trial.

We will be in touch with you with regards to an API key to unlock your integration.

The endpoints you need to continue are below.

{% table %}
| Environment | URL | 
| ---- | ---- | 
| Sandbox | &lt;a href="http://demo.api.yotisign.com/"&gt;demo.api.yotisign.com&lt;/a&gt; | 
| Production | &lt;a href="http://api.yotisign.com/"&gt;api.yotisign.com&lt;/a&gt; | 
{% /table %}

---

## Security

If you believe your Key has been compromised, please contact us as soon as possible. This can be done through your account manager or via our support support by emailing [sdksupport@yoti.com](mailto:sdksupport@yoti.com).

It is important to note that your API Key is strictly confidential to you and should be stored securely. It is never advisable to commit any code containing your API Key and it should never be shared beyond the authorised party.

---

## Step 2: Creating a Sign Request

The endpoint allows you to create a sign request by sending a document through to the Yoti Sign service. You will need to pinpoint on the document where you would like the signees e-signature.

{% table %}
| Endpoint | 
| ---- | 
| POST /sign-requests | 
{% /table %}

Constructing a document requires the following:

{% table %}
| Parameter | Description | 
| ---- | ---- | 
| Authorization&lt;br&gt;(header) | Your API Key is required on all calls to the API and should be sent as a bearer token. | 
| Content-Type&lt;br&gt;(header) | application/x-www-form-urlencoded | 
| file&lt;br&gt;(formData) | This is the PDF of the document that needs signing. | 
| file_name&lt;br&gt;(formData) | The name of the document to be signed. | 
| email&lt;br&gt;(formData) | The email parameters lets you specify a message to be sent to a signee. See example below. | 
| recipients&lt;br&gt;(formData) | Recipients contains an array of signees, this is used to specify exactly where each signee must e-sign on a given document.&nbsp;See example below. | 
| custom_webhook_uri | Specifies an endpoint to send updates to when documents are signed. This avoids the need to poll the Get sign request endpoint. | 
{% /table %}

### Example email object

In order to create a sign request, the API will require an invitation object and message. This message will be sent within the email sent to your signees.

{% code %}
{% tab language="json" %}
'{
  "invitation": {
    "message": "Please sign the example document"
  }
}'
{% /tab %}
{% /code %}

### Example recipients array

You will also need to specify an array of JSON objects to define the intended signees. This array can hold up to **10** signees.

{% table %}
| Parameter (Recipients) | Description | 
| ---- | ---- | 
| name | This should be a string with a maximum length of 100 characters. The name specifies the name of the target signee. | 
| email | This should be a string with a maximum length of 100 characters. The email specifies the email address of the target signee. | 
| role | String value of role of the signee, this is free text and can be used to identify the role of the signee, the maximum length is 50 characters. | 
| auth_type | auth_type can be one of either "sign&lt;i&gt;_&lt;/i&gt;auth" or "no_auth". If "sign_auth" is selected a Yoti scan will be required, email_address is added by default to the list of Yoti attributes even if no attributes are provided.&lt;br&gt; | 
| yoti_attributes | &lt;p&gt;Possible Yoti attributes are:&lt;/p&gt;&lt;p&gt;&nbsp;[ postal_address, selfie, full_name, date_of_birth, gender, nationality, phone_number ]&lt;br&gt;&lt;/p&gt; | 
| tags | A tag is an array of objects used to place signature fields on a given PDF. To populate a tag, you will need to specify a page number, x and y co-ordinate, and a tag type. You may specify up to 10 tags per signee. | 
{% /table %}

{% table %}
| Parameter (tags) | Description | 
| ---- | ---- | 
| page_number | This marks the page number of the page to place a tag. | 
| x | The 'X' co ordinate of the tag field, this is a decimal number starting from the top left of the page. Minimum value can be 0 and maximum of 0.949. | 
| y | The 'Y' co-ordinate of the tag field, this is a decimal number starting from the top left of the page. Minimum value can be 0 and maximum of 0.95. | 
| width | If text_field is selected as type, a width must be provided. This is not required for signature. The width sets the width of the text_field and can be a minimum of 0.05. The maximum width of the text field should be less than 1.0 when added to the x co-ordinate value. | 
| type | This should be set to either "text_field" or "signature". Setting the type to "text_field" allows a signee to enter free text, a width value must be specified alongside "text_field" to define the size of the field. "signature" is used to indicate a click to sign box.&lt;br&gt; | 
{% /table %}

{% code %}
{% tab language="json" %}
'[
  {
    "name": "Alice",
    "email": "alice@example.com",
    "role": "Signee",
    "auth_type": "sign-auth",
    "yoti_attributes": ["full_name"],
    "tags": [
      {
        "page_number": "1",
        "x": "0.28533816425120773",
        "y": "0.36558678479931683",
        "type": "signature"
      }
    ]
  },
  {
    "name": "Jack",
    "email": "Jack@example.com",
    "role": "Signee",
    "tags": [
      {
        "page_number": "2",
        "x": "0.3932",
        "y": "0.4234",
        "type": "signature"
      }
    ]
  }
]'
{% /tab %}
{% /code %}

Below is a complete example of how to construct a request to the Create Sign Request endpoint.

{% code %}
{% tab language="javascript" %}
const rp = require('request-promise');

const fs = require('fs');

const createSignRequest = () => {
    const email = {
        invitation: {
            message: 'Please sign the example document', // message to send to signee
        },
    };

    const recipients = [
        {
            name: 'John Smith', // name of signee
            email: 'example@example.com', // email of signee
            role: 'Signee', // role of signee
            tags: [
                {
                    page_number: '1', // page number of document where signature required
                    x: '0.3', // x co-ordinate of page to place signature
                    y: '0.4', // y co-ordinate of page to place signature
                    type: 'signature', // type of signing required
                },
            ],
        },
    ];

	const webHookUrl = YOUR_WEBHOOK_URL; // your webhook url

    const options = {
        method: 'POST',
        uri: `${process.env.BASE_URL}/v1/sign-requests`, // url of API
        formData: {
            file: fs.createReadStream('./pdf-sample/test.pdf'), // file system location of PDF
            file_name: 'Example Document', // name to call file
            email: JSON.stringify(email),
            recipients: JSON.stringify(recipients),
			custom_webhook_uri: webHookUrl // OPTIONAL if webhook url specified
        },
        headers: {
            authorization:
                `Bearer ${process.env.API_KEY}`, // API key
        },
    }

    return rp(options)
        .then(body => body)
        .catch(err => err);
};

(async () => {
    let result = await createSignRequest();
    // handle result
})();
{% /tab %}
{% /code %}

On success we return a 200 and a JSON object in the following format:

{% code %}
{% tab language="json" %}
{
  "status": "QUEUED",
  "url": "https://api.yotisign.com/v1/sign_requests/{sign_request_id}"
}
{% /tab %}
{% /code %}

The `sign_request_id` returned is the unique identifier for this specific created request. You should store this as it may be used to Archive Requests, retrieve the status, or Get the Completed Document.

### WebHook

It is possible to specify a WebHook URL so that you can be informed of updates to Yoti Sign documents as they happen.

The Yoti Sign system will send a POST request to the specified endpoint as described in the above table. An example of the response from the WebHook is listed below.

{% code %}
{% tab language="json" %}
{
  "sign_request_id": "d7df4273-0087-4866-ac1d-a21640b813e8",
  "request_status": "COMPLETE",
  "recipients": [
    {
      "id": "2cf6e424-faa1-4ddf-a4ec-8b4b21d513f0",
      "label": "Signee",
      "signed_at": "2019-10-18T10:37:33.843Z"
    }
  ],
  "documents": [
    {
      "name": "Document.pdf"
    }
  ]
}
{% /tab %}
{% /code %}

### Other response codes

{% table %}
| Response | Description | 
| ---- | ---- | 
| 401 | 401 is returned if a request is unauthorised. This is likely due to the API Key either being incorrect or not being sent properly in the headers. The key should be sent as a Bearer token over the authorisation header. | 
{% /table %}

## Step 3: Archive a Sign Request

Sign Requests can be archived**.** The API exposes an Archive Sign Request endpoint to achieve this:

{% table %}
| Endpoint | 
| ---- | 
| PATCH /sign-requests/{sign_request_id}&lt;br&gt; | 
{% /table %}

{% table %}
| Parameter | Description | 
| ---- | ---- | 
| Authorization&lt;br&gt;(header) | Your API Key is required on all calls to the API and should be sent as a bearer token. | 
| Content-Type&lt;br&gt;(header)&lt;br&gt; | application/json | 
| Body&lt;br&gt;(body) | Archiving a Sign Request requires you to send a status of "ARCHIVED" in the body of your request&lt;br&gt;&lt;code class="inline-code"&gt;{&lt;/code&gt;&lt;br&gt;&lt;code class="inline-code"&gt;&nbsp; &nbsp; "status": "ARCHIVED"&lt;/code&gt;&lt;br&gt;&lt;code class="inline-code"&gt;}&lt;/code&gt; | 
| &lt;font color="#444444"&gt;&lt;span&gt;sign_request_id&lt;br&gt;&lt;/span&gt;&lt;/font&gt;&lt;p&gt;&lt;font color="#444444"&gt;&lt;span&gt;(path)&lt;/span&gt;&lt;/font&gt;&lt;/p&gt; | This is a UUID referring to the Sign Request you are looking to archive. This will be the UUID obtained from the Create Sign Request endpoint | 
{% /table %}

A complete example of how to archive a sign request can be found below.

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

The Archive Sign Request endpoint returns a status code of 204 if successful.

### Other response codes

{% table %}
| Response | Description | 
| ---- | ---- | 
| 400 | The API returns a 400 if the parameter sent to it is incorrect. You may only send a status of 'ARCHIVED' or the request will be unsuccessful. | 
| 401 | 401 is returned if a request is unauthorised. This is likely due to the API Key either being incorrect or not being sent properly in the headers. The key should be sent as a Bearer token over the authorisation header. | 
| 404 | If the request&nbsp;is not found you will receive a 404. This will be due to the request ID being invalid. | 
{% /table %}

## Step 4: Get a Sign Request

Checking the status of a Sign Request is achieved through the GET sign request endpoint.

{% table %}
| Endpoint | 
| ---- | 
| GET /sign-requests/{sign_request_id} | 
{% /table %}

{% table %}
| Parameter | Description | 
| ---- | ---- | 
| Authorization&lt;br&gt;(header) | Your API Key is required on all calls to the API and should be sent as a bearer token. | 
| &lt;p&gt;Content-Type&lt;br&gt;(header)&lt;/p&gt; | application/json | 
| sign_request_id&lt;br&gt;(path) | This is a UUID referring to the Sign Request you are looking to retrieve. This will be the UUID obtained from the Create Sign Request endpoint | 
{% /table %}

A complete example of how to GET the status of a sign request can be found below.

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

On success, we return a 200 with a JSON body matching the following schema

{% table %}
| Response | Description | 
| ---- | ---- | 
| id | The unique request ID to identify the sign request. | 
| completed_at | Once all signees have signed the document it is marked as COMPLETE, the completed_at field stores the timestamp of when the last signee completes the request. | 
| status | The status of a sign request can either be "COMPLETE", "ACTIVE" or "ARCHIVED. A sign request defaults to "ACTIVE" and will remain in this state until all signees have signed the document. Once it is fully signed the state will update to "COMPLETE". A status may be "ARCHIVED" if you archive a document using the archive sign request endpoint. | 
| file_name | The name of the document as specified in the create sign request body. | 
| completed_file&lt;i&gt;_&lt;/i&gt;location&lt;br&gt; | This is the location of the completed document, this URL may be used with valid authentication to retrieve the completed document at a later date. | 
| recipients | An array containing the list of signees and a breakdown of their status in regards to the sign request. | 
{% /table %}

{% table %}
| Response (Recipients) |  | 
| ---- | ---- | 
| id&lt;br&gt; | Used to identifier who has signed this document. | 
| sign_status | The sign_status may be one of either "SIGNED" or "UNSIGNED" | 
| role | The role is returned as specified when creating the sign request. | 
| signed_at | A timestamp indicating when the signee signed the document. | 
| name | The name of the signee. | 
| email | The email address of the signee. | 
| yoti_attributes | If the sign request was sent to a signee requesting yoti_attributes, the list of signed attributes are returned, this an array of any of the following values [postal_address, selfie, full_name, date_of_birth, gender, nationality, phone_number].&lt;br&gt; | 
{% /table %}

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

### Other response codes

{% table %}
| Response | Description | 
| ---- | ---- | 
| 401 | 401 is returned if a request is unauthorised. This is likely due to the API Key either being incorrect or not being sent properly in the headers. The key should be sent as a Bearer token over the authorisation header. | 
| 404 | If the request is not found you will receive a 404. This will be due to the request ID being invalid. | 
{% /table %}

## Step 5: Get a Completed Document

Once signed, a full copy of the completed document can be obtained by calling into the Get Completed Document endpoint. This returns a PDF.

{% table %}
| Endpoint | 
| ---- | 
| GET /sign-requests/{sign_request_id}/completed-documents | 
{% /table %}

{% table %}
| Parameter | Description | 
| ---- | ---- | 
| Authorization&lt;br&gt;(header) | Your API Key is required on all calls to the API and should be sent as a bearer token. | 
| Content-Type&lt;br&gt;(header) | application/pdf | 
| sign_request_id&lt;br&gt;(path) | This is a UUID referring to the Completed Document you are looking to retrieve. This will be the UUID obtained from the Create Sign Request endpoint | 
{% /table %}

A complete example of how to Get a document Document can be found below.

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

On success, this endpoint returns a status code of 200 with the document as a PDF.

### Other response codes

{% table %}
| Response | Code | 
| ---- | ---- | 
| 401 | 401 is returned if a request is unauthorised. This is likely due to the API Key either being incorrect or not being sent properly in the headers. The key should be sent as a Bearer token over the authorisation header. | 
| 404 | If the requested document is not found you will receive a 404. This will be due to the request ID being invalid. | 
{% /table %}