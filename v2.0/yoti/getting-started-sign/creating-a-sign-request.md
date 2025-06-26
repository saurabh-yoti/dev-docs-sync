---
type: page
title: Creating a sign request
listed: true
slug: creating-a-sign-request
description: 
index_title: Creating a sign request
hidden: 
keywords: 
tags: 
---

The endpoint allows you to [create a sign request](https://yoti.com/api-reference/#yoti-sign-creating-a-sign-request) by sending a PDF document through to the Yoti Sign service.

## Creating a sign request endpoint

Below is the end point used for creating a sign request.

{% code %}
{% tab language="http" %}
Sandbox POST https://demo.api.yotisign.com/v1/sign-requests 
Production POST https://api.yotisign.com/v1/sign-requests
{% /tab %}
{% /code %}

This service will send an email to the signee prompting them through the Yoti Sign flow. There is a configurable option to customise the signing request message that gets sent.

{% image url="https://res.cloudinary.com/developerhub/image/upload/v1572534062/22175/joyepbj3s5pz0hzq4llf.jpg" caption="Document received to sign" mode="600" height="596" width="745" %}
{% /image %}

## Example email object

In order to [create a sign request](https://yoti.com/api-reference/#yoti-sign-creating-a-sign-request) the API will require an invitation object and message. This message will be sent within the email sent to your signees.

{% code %}
{% tab language="json" %}
'{
  "invitation": {
    "message": "Please sign the example document"
  }
}'
{% /tab %}
{% /code %}

The following elements are configurable:

{% table %}
| Parameter | Description | 
| ---- | ---- | 
| Authorization (header) | API Key to call the Yoti Sign API.\n\nThis should be sent as a bearer token. | 
| Content-Type (header) | multipart/form-data. | 
| file (formData) | The PDF document that requires signing. | 
| file_name (formData) | The name of the document to be signed. | 
| email (formData) | The email parameter lets you specify a message to be sent to a signee. See example above. | 
| recipients (formData) | Recipients contains an array of signees, this is used to specify exactly where each signee must e-sign on a given document. See example below. | 
| custom_webhook_uri (formData) | Specifies an endpoint to receive updates when documents are signed. Webhooks retry 10 times, with a delay of 30 seconds between each try. Endpoint must be HTTPS with TLS only and not HTTP. | 
{% /table %}

## Example recipients array

Here is where you will need provide an array of JSON objects to define the intended signees of the document. This array can hold up to **10** signees.

{% code %}
{% tab language="json" %}
'[
  {
    "name": "Alice",
    "email": "alice@example.com",
    "role": "Signee",
    "auth_type": "sign-auth",
    "yoti_attributes": ["full_name"],
	"sign_group": "2",
    "tags": [
      {
        "page_number": "1",
        "x": "0.28533816425",
        "y": "0.36558678479",
        "type": "signature"
      },
      {

        "page_number": "1",
        "x": "0.3",
        "y": "0.4",
        "type": "text_field",
        "optional": true
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

{% table %}
| Parameter (Recipients) | Description | 
| ---- | ---- | 
| name | This should be a string with a maximum length of 100 characters. The name specifies the name of the target signee. | 
| email | This should be a string with a maximum length of 100 characters. The email specifies the email address of the target signee. | 
| role | String value of role of the signee, this is free text and can be used to identify the role of the signee, the maximum length is 50 characters. | 
| auth_type | auth_type can be one of either "sign-auth" or "no-auth". If "sign-auth" is selected a Yoti scan be be required.\n\n\nThe email_address attribute is added by default to the list of Yoti attributes even if no attributes are provided. | 
| yoti_attributes | Possible Yoti attributes are:\n\n\n\n[ postal_address, selfie, full_name, date_of_birth, gender, nationality, phone_number ] | 
| sign_group | String value between 1 and 10. This defines an order in which recipients receive invitations to sign a document. For example, all recipients within sign group 1 will be the first to receive a document to sign. Once all recipients from sign group 1 have signed, the document will be sent to sign group 2. If no sign group is specified, a default of 1 will be assumed. | 
| tags | A tag is an array of objects used to place signature fields on a given PDF. To populate a tag, you will need to specify a page number, x and y co-ordinate, and a tag type. You may specify up to 10 tags per signee. | 
{% /table %}

{% html %}
<div class="alert-know">
    <div class="alert-title" id="know">
        Knowledge base
    </div>
    <div class="alert-text">
For more information on the the Yoti attributes head over to our Knowledge base.
    </div>
    <div class="alert-links"> 
       <a href="https://developers.yoti.com/yoti/knowledge-base-hub#yoti-attributes-explained">Yoti Attributes explained</a>
    </div>
</div>
{% /html %}

Within the tag array you can specify the following:

{% table %}
| Parameter (tags) | Description | 
| ---- | ---- | 
| page_number | This marks the page number of the page to place a tag. | 
| x | The 'X' co ordinate of the tag field, this is a decimal number starting from the top left of the page. Minimum value can be 0 and maximum of 0.949. | 
| y | The 'Y' co-ordinate of the tag field, this is a decimal number starting from the top left of the page. Minimum value can be 0 and maximum of 0.95. | 
| width | If text_field is selected as type, a width must be provided. This is not required for signature. The width sets the width of the text field and can be a minimum of 0.05. The maximum width of the text field should be less than 1.0 when added to the x co-ordinate value. | 
| type | This should be set to either "text_field" or "signature". Setting the type to "text___field" allows a signee to enter free text, a width value must be specified alongside "text_field" to define the size of the field. "signature" is used to indicate a click to sign box. | 
| optional | A tag can be marked as "optional" by adding the "optional" parameter. If a tag is marked as "optional" a recipient will be allowed to sign the document without submitting the tag. If an "optional" tag is not submitted by a signer, the tag will not show up on the completed document. The default value is "false". `yoti_attributes` may not be marked as "optional". | 
{% /table %}

## Reminders Object

You can configure reminders to be sent to recipients who still have active documents that need signing. There will be 3 reminders (this is not currently configurable) that will be sent out with a frequency of 1, 2 or 7 days.

{% code %}
{% tab language="json" %}
"reminders": {
        "frequency": 1
    }
{% /tab %}
{% /code %}

## Complete Example

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
  
  const reminders = { //reminder emails to be sent to the recipient
    frequency: '1' //days between reminders
  }
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

On success Yoti returns a 200 and a JSON object in the following format:

{% code %}
{% tab language="json" %}
{
  "status": "QUEUED",
  "url": "https://api.yotisign.com/v1/sign_requests/{sign_request_id}"
}
{% /tab %}
{% /code %}

{% html %}
<div class="alert-GTK">
    <div class="alert-title" id="GTK">
        Good to know... 
    </div>
    <div class="alert-text">
        The sign_request_id returned is the unique identifier for this specific created request. You should store this as it can 
be used to Archive Requests, Retrieve the Status, or Get the Completed Document.
   </div>
</div>
{% /html %}

## Webhook

It is possible to specify a WebHook URL to be informed of updates to Yoti Sign documents as they happen.

The Yoti Sign system will send a POST request to the specified endpoint as described in the above table. An example of the response from the WebHook is listed below.

{% html %}
<div class="alert-GTK">
    <div class="alert-title" id="GTK">
        Good to know... 
    </div>
    <div class="alert-text">
        Please note that Webhooks retry 10 times, with a delay of 30 seconds between each try. Only HTTPS endpoints with TLS are supported. The HTTPS endpoint can be self signed when using the sandbox demo API, however endpoints in production require fully verified HTTPS.
    </div>
</div>
{% /html %}

### 'Success' Webhook

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

### 'Errors' Webhook

The Yoti Sign API will send a webhook notification if there is a problem during the creation of the sign request. The payload for this type of notification looks like this:

{% code %}
{% tab language="json" %}
{

     "id": sign request id,
     "status": "ERRORED",
     "code": error code as described below
}
{% /tab %}
{% /code %}

If a webhook notification has been received, you may use it to query for a human readable message by [getting the status](/yoti/status-of-sign-request) of the envelope. Below are the error codes and their descriptions.

### Errors codes

{% table %}
| Code | Description | How to fix | 
| ---- | ---- | ---- | 
| `PASSWORD_PROTECTED` | The PDF is password protected | Remove the password protection and try again | 
| `MALICIOUS_PDF` | The PDF contains executable javascript | Remove the javascript and try again | 
| `PDF_READER` | The PDF file cannot be read. It may be corrupted | Please try to recreate your PDF and try again | 
| `WORD_DOC_CONV_ERROR` | The Word document is corrupt, or has been password protected | Repair the corrupt document, or remove the password protection from the Word Doc and try again | 
| `NO_PAGE_FOR_TAG_ERROR` | You have specified a tag that has been assigned to a page that does not exist | Please check that the PDF has the page that you specified for the tags | 
{% /table %}

## Other response codes

{% table %}
| Response | Description | 
| ---- | ---- | 
| 401 | 401 is returned if a request is unauthorised. This is likely due to the API Key either being incorrect or not being sent properly in the headers. The key should be sent as a Bearer token over the authorisation header. | 
{% /table %}