---
type: page
title: Create envelope
listed: true
slug: create-an-envelope-request
description: 
index_title: Create envelope
hidden: 
keywords: 
tags: 
---

An envelope serves as a container for all Yoti Sign transactions. Inside an envelope is information about a specific transaction, including:

{% image url="https://res.cloudinary.com/developerhub/image/upload/v1589460567/28180/sdfqjgcrkv2smcxsrr8i.png" caption="Envelope" mode="responsive" height="258" width="1590" %}
{% /image %}

The endpoint allows you to create an envelope request by sending one or more documents through to the Yoti Sign service.

{% code %}
{% tab language="http" title="" %}
Sandbox POST https://demo.api.yotisign.com/v2/envelopes 

Production POST https://api.yotisign.com/v2/envelopes
{% /tab %}
{% /code %}

When you create an envelope the following elements are configurable:

- [File](/yoti-sign/create-an-envelope-request#file-types)
- [Name](/yoti-sign/create-an-envelope-request#-name-object-)
- [Email](/yoti-sign/create-an-envelope-request#-email-object-)
- [Recipients](/yoti-sign/create-an-envelope-request#-recipient-object-)
- [Notifications](/yoti-sign/create-an-envelope-request#notifications)

---

## Headers explained

The following elements are needed in the header:

{% table %}
| Header | Description | 
| ---- | ---- | 
| Authorization | API Key to call the Yoti Sign API. This should be sent as a bearer token. | 
| Content-Type | multipart/form-data | 
{% /table %}

---

## Body explained

Jump straight to the bottom of this page for the [full request.](https://developers.yoti.com/yoti/create-an-envelope-request#full-request)

Each subpart should declare its appropriate **Content-Type:**

{% table %}
| Field | Description | 
| ---- | ---- | 
| file | Supported file types with content-type header with content-type header | 
| options | application/json | 
{% /table %}

### File types

Yoti Sign supports the following document formats:

- pdf (application/pdf)
- .docx (application/vnd.openxmlformats-officedocument.wordprocessingml.template)
- .doc (application/msword)

There must be at least 1 file and a maximum of 20. When sending multiple documents, they will be received in the order sent. 

{% html %}
<div class="alert-BYS">

   <div class="alert-title" id="BYS">

Havent got your API Key?
   </div>

   <div class="alert-text" >

      Request your API keys, please let us know if you want to use sandbox or production. 

   </div>

   <div class="alert-links"> 

         <a href="https://www.yotisign.com/app/contact-us/">Get API keys</a>

   </div>

</div>
{% /html %}

## Options object

**Name property**

This is the name of the envelope. It will be presented as the email subject and the document tag in the email.

{% code %}
{% tab language="json" %}
{
    "name": "envelope name",
}
{% /tab %}
{% /code %}

{% table %}
| Parameter | Description | 
| ---- | ---- | 
| name | This must be between 1 and 65 characters | 
{% /table %}

**Email object**

This service will send an email to the recipient prompting them through the Yoti Sign flow. There is a configurable option to customise the signing request message that gets sent. The API will require an invitation object and message. This message will be included within the email sent to your recipients.

{% code %}
{% tab language="json" %}
{
    "emails": {
        "invitation": {
            "body": {
                "message": "Please sign this document"
            }
        }
    },
}
{% /tab %}
{% /code %}

{% image url="https://res.cloudinary.com/developerhub/image/upload/v1590497199/29786/bmiy1dxdq2hnbb8jz7ew.jpg" caption="Body > Email object" mode="responsive" height="552" width="629" %}
{% /image %}

{% table %}
| Parameter | Description | 
| ---- | ---- | 
| emails | The email parameter lets you specify a message to be sent to a recipient. See example above. | 
| message | The message that appears the bottom of the email or template with instructions for the user. This must be between 1 and 600 characters | 
{% /table %}

---

## Recipient object

Here is where you will need to provide an array of JSON objects to define the intended recipient of the document. This array can hold up to **10** recipients.

{% code %}
{% tab language="json" %}
{
    "name": "envelope name",
    "emails": {
        "invitation": {
            "body": {
                "message": "Please sign this document"
            }
        }
    },
    "recipients": [
        	{
            "name": "User 1",
            "email": "user1@test.com",
            "role": "CEO",
            "auth_type": "no-auth",
            "sign_group": 1,
            "tags": [
                {
                    "page_number": 1,
                    "x": 0.1,
                    "y": 0.1,
                    "type": "signature",
                    "optional": false,
                    "file_name": "myfile.pdf"
                }
							]
						},
						{
            "name": "User 2",
            "email": "user2@test.com",
            "role": "CPO",
            "auth_type": "sign-auth",
            "yoti_attributes": ["full_name"],
            "sign_group": 2,
            "tags": [
                {
                    "page_number": 1,
                    "x": 0.6,
                    "y": 0.3,
                    "type": "signature",
                    "optional": false,
                    "file_name": "myfile.pdf"

                	}
            	]
        		}
    ],
    "notifications": {
        "destination": "https://mysite.example/events",
        "subscriptions": [
            "envelope_completion"
        ]
    }
}
{% /tab %}
{% /code %}

{% table %}
| Parameters | Description | 
| ---- | ---- | 
| name | This should be a string and should not be less than 1 character with a maximum length of 100 characters. The name specifies the name of the target recipient. | 
| email | The email specifies the email address of the target recipient. This must be a valid email address (RFC 5322). | 
| role | String value of role of the recipient, this is free text and can be used to identify the role of the recipient, the maximum length is 50 characters. | 
| auth_type | Auth_type can be one of either \n\n\n\n- "no-auth": A digital signature is required. \n- "sign-auth": A Yoti scan will be required for this signature.\n\n\nThe email_address attribute is added by default to the list of Yoti attributes even if no attributes are provided. | 
| yoti_attributes | If you select sign-auth the list of Yoti attributes that can be used are:\n\n\nfull_name,\n\n\n\nemail_address - This is enabled by default,\n\n\ndate_of_birth,\n\n\n\npostal_address,\n\n\n\ngender,\n\n\n\nnationality,\n\n\n\nphone_number,\n\n\n\nphoto. | 
| sign_group | This defines an order in which recipients receive invitations to sign a document. \n\nFor example, all recipients within sign group 1 will be the first to receive a document to sign. Once all recipients from sign group 1 have signed, the document will be sent to sign group 2. There must be at least 1 sign_group, and the order must be sequential, starting from 1. | 
{% /table %}

---

### Tags explained

A tag is an array of objects used to place signature fields on a given document as shown above.

To populate a tag, you will need to specify a page number, x and y co-ordinate, and a tag type. There is a limit of 200 tags per recipient. A recipient can have 0 tags.

{% table %}
| Parameter | Description | 
| ---- | ---- | 
| page_number | This marks the page number of the page to place a tag. This must correspond to a page number on the file designated by the **file_name** provided for the tag. If it does not match the envelope will not be created. | 
| x | The 'X' co-ordinate of the tag field, this is a decimal fraction of the page width. Minimum value can be 0 and maximum of 0.949. | 
| y | The 'Y' co-ordinate of the tag field, this is a decimal fraction of the page height. Minimum value can be 0 and maximum of 0.949. | 
| type | This should be set to either \n\n "text_field", "signature", "checkbox_field", "radio_field", "date_signed_field".\n\n\n\n"text_field" allows a recipient to enter free text, a width value must be specified alongside "text field" to define the size of the field. Width is only applied to "text_field" and must be greater than 0.\n\n\n"signature" is used to indicate a click to sign box.\n\n\n\n"checkbox_field" is used to generate a check box for the user to select.\n\n\n\n"radio_field" is used to generate a radio button for the user to select. For multiple "radio_fields", these can be grouped using "tag_group_name".\n\n\n\n"date_signed_field" if selected is auto generated by Yoti Sign to apply the date of when the signer submitted their signature to the document, in the position that a sender sets up during the sender flow. This is in UTC format and is not a manual input field. | 
| optional | A tag can be marked as "optional" by adding the "optional" parameter. If a tag is marked as "optional" a recipient will be allowed to sign the document without submitting the tag. If an "optional" tag is not submitted by a sender, the tag will not show up on the completed document. `yoti_attributes` may not be marked as "optional". | 
| filename | The name of the document to be signed and must correspond to a filename of one of the files provided in the request (including the file extension). The character limit is 255. \nIf it does not match, the envelope will not be created, | 
| tag_group_name | Used to group multiple tags of the same type. Grouping radio fields by a tag group ensures only one radio field can be selected out of the group. | 
{% /table %}

### Auto Tagging

You can add a tag to your template document using our auto tagging feature by inserting an anchor into your document. An anchor is made of:

- A Role
- Recipient number 
- Tag Type
- Required/Optional

{% table %}
| Anchor Type | Example | Description | 
| ---- | ---- | ---- | 
| Role | Signer `(S)` | Role of the recipient | 
| Recipient number | x`(1 to 8)` | Number of recipients. This must be a number from 1 to 8. | 
| Tag Type | Signature `(S)` | Type of field. See above for more details. | 
| Required / Optional | Required `(R)` or Optional `(O)` | If you require the recipient to complete this transaction in order to sign the document. | 
| Header tag | &#124;AT&#124; | Place this on the first page of your document to signify that the document contains auto tags. | 
{% /table %}

An example of an anchor is:

{% code %}
{% tab language="json" %}
| <Role> <Tag Type> <Required> |

|S1SR| //Signer 1, Signature, Required
|G4TO| //Guarantor 4 , Text field, Optional
{% /tab %}
{% /code %}

**Enabling Auto Tagging**

To use the auto tagging feature you will first have to enable this in your options object. You will need to set the Industry Type based on the Signer Roles you wish to use. Please see the table below. 

PLEASE NOTE: You will have to leave the tags property in your recipients object. This can be empty.

{% code %}
{% tab language="json" %}
{
    "name": "envelope name",

   {
    "name": "envelope name",
    "autotagging": "GENERAL", //Industry Type
    "emails": {
        "invitation": {
            "body": {
                "message": "Please sign this document"
            }
        }
    },
    "recipients": [
        	{
            "name": "User 1",
            "email": "user1@test.com",
            "role": "Signer 1", //This must match the tag anchor on your document
            "auth_type": "no-auth",
            "sign_group": 1,
            "tags": [] //This should be present but empty
						},
{% /tab %}
{% /code %}

A list of the roles Yoti Sign offers:

{% table %}
| Roles | Tag | Industry Type | 
| ---- | ---- | ---- | 
| Signer | S | GENERAL | 
| Tenant | T | REAL_ESTATE | 
| Landlord | L | REAL_ESTATE | 
| Agent | A | REAL_ESTATE | 
| Guarantor | G | REAL_ESTATE | 
{% /table %}

A list of the tag types Yoti Sign offers:

{% table %}
| Tag Types | Tag | Example | 
| ---- | ---- | ---- | 
| Signature | S | S1SR | 
| Text Field | T | S1TR | 
| Check Box | CB | S1CBR | 
| Date Signed | DS | S1DSR | 
| Radio Group | RG[X]* | S1RG1R | 
{% /table %}

- A group number must be provided for radio group tags. This ensures only one radio field per group number is selectable.

{% html %}
<div class="alert-BYS">

   <div class="alert-title" id="BYS">

Auto tagging matrix
   </div>

   <div class="alert-text" >

      Make sure that your tags are formatted correctly by viewing the auto tagging matrix.

   </div>

   <div class="alert-links"> 

         <a href="https://www.yoti.com/wp-content/uploads/Sign_Auto-tagging-matrix.pdf">View matrix</a>

   </div>

</div>
{% /html %}

---

### Notifications

You can subscribe to notifications which will be sent to a specified endpoint. This endpoint will need to be publicly accessible.

{% code %}
{% tab language="json" %}
"notifications": {
        "destination": "https://mysite.com/events",
        "subscriptions": [
            "envelope_completion"
       ]
    }
{% /tab %}
{% /code %}

{% table %}
| Notification | Description | 
| ---- | ---- | 
| destination | scheme of the URL must be HTTPS and a discrete parameter | 
| envelope_completion | When all recipients have signed. | 
| upload_errors | When there is an error in the envelope creation process | 
{% /table %}

### Reminders

You can configure reminders to be sent to recipients who still have active documents that need signing. There will be 3 reminders (this is not currently configurable) that will be sent out with a frequency of 1, 2 or 7 days.

{% code %}
{% tab language="json" %}
"reminders": {
        "frequency": 1
    }
{% /tab %}
{% /code %}

---

## Full request

Below is an example of the full request for creating an envelope. 

{% code %}
{% tab language="json" %}
{
    "name": "envelope name",
    "emails": {
        "invitation": {
            "body": {
                "message": "Please sign this document"
            }
        }
    },
    "recipients": [
        	{
            "name": "User 1",
            "email": "user1@test.com",
            "role": "CEO",
            "auth_type": "no-auth",
            "sign_group": 1,
            "tags": [
                {
                    "page_number": 1,
                    "x": 0.1,
                    "y": 0.1,
                    "type": "signature",
                    "optional": false,
                    "file_name": "myfile.pdf"
                }
							]
						},
						{
            "name": "User 2",
            "email": "user2@test.com",
            "role": "CPO",
            "auth_type": "sign-auth",
            "yoti_attributes": ["full_name"],
            "sign_group": 2,
            "tags": [
                {
                    "page_number": 1,
                    "x": 0.6,
                    "y": 0.3,
                    "type": "signature",
                    "optional": false,
                    "file_name": "myfile.pdf"

                	}
            	]
        		}
    ],
    "notifications": {
        "destination": "https://mysite.example/events",
        "subscriptions": [
            "envelope_completion"
        ]
    }
}
{% /tab %}
{% /code %}

## Example code

{% code %}
{% tab language="javascript" %}
const rp = require("request-promise");
const fs = require("fs");

const options = {}; //options object

const createEnvelope = () => {
  const request = {
    method: "POST",
    uri: `<BASE_URL>/v2/envelopes`,
    formData: {
      file: fs.createReadStream("path/to.pdf"),
      options: JSON.stringify(options),
    },
    headers: {
      authorization: "Bearer <API_KEY>",
    },
  };

  return rp(request)
    .then((body) => body)
    .catch((err) => err);
};

//send request
let result = await createEnvelope();
{% /tab %}
{% tab language="java" %}
package com.yoti.sign;

import java.io.File;
import java.io.IOException;
import java.net.URI;

import javax.json.Json;
import javax.json.JsonObject;
import javax.json.JsonReader;

import org.apache.http.HttpResponse;
import org.apache.http.client.methods.HttpPost;
import org.apache.http.entity.ContentType;
import org.apache.http.entity.mime.MultipartEntityBuilder;
import org.apache.http.impl.client.CloseableHttpClient;
import org.apache.http.impl.client.HttpClients;

public class Example {

    private static final String YOTI_SIGN_AUTH_TOKEN = "<YOUR_AUTH_TOKEN>";
    private static final String YOTI_SIGN_BASE_URL = "https://api.yotisign.com/v2";

    public static void main(String[] args) {
        
        // Create the client and HttpRequest
        CloseableHttpClient client = HttpClients.createDefault();
        HttpPost httpPost = new HttpPost();
        
        URI uri = URI.create(YOTI_SIGN_BASE_URL + "/envelopes");
        httpPost.setURI(uri);
        
        // Set the 'Authorization' header
        httpPost.setHeader("Authorization", "Bearer " + YOTI_SIGN_AUTH_TOKEN);

        // Create a Multipart request entity, and add the file to send
        // along with the options
        MultipartEntityBuilder formDataBuilder = MultipartEntityBuilder.create();

        File file = new File("/path/to/your/file.pdf");
        formDataBuilder.addBinaryBody("file", file);

        String jsonPayload = ...; // JSON string containing the options
        formDataBuilder.addTextBody("options", jsonPayload, ContentType.APPLICATION_JSON);
        
        // Add the Multipart request entity to the Http request
        httpPost.setEntity(formDataBuilder.build());        

        try {
            // Perform the POST request and read the created envelope ID
            HttpResponse response = client.execute(httpPost);

            JsonReader reader = Json.createReader(response.getEntity().getContent());
            JsonObject responseObject = reader.readObject();

            String envelopeId = responseObject.getString("envelope_id");
        } catch (IOException e) {
            e.printStackTrace();
        }
    }

}
{% /tab %}
{% tab language="php" %}
<?php

use GuzzleHttp\Client;
use GuzzleHttp\Psr7\MultipartStream;
use GuzzleHttp\Psr7\Request;

use function GuzzleHttp\Psr7\stream_for;

$options = [
    'file_name' => 'example-document.pdf',
    'name' => 'Sign your request for..',
    'emails' => [
        'invitation' => [
            'body' => [
                'message' => 'Please sign the example document',
            ],
        ],
    ],
    'recipients' => [
        [
            'name' => 'John Smith',
            'email' => 'example@example.com',
            'role' => 'Signee',
            'auth_type' => 'no-auth',
            'sign_group' => 1,
            'tags' => [
                [
                    'page_number' => 1,
                    'x' => 0.3,
                    'y' => 0.4,
                    'type' => 'signature',
                    'optional' => false,
                    'file_name' => 'example-document.pdf',
                ],
            ],
        ],
    ],
    'custom_webhook_uri' => YOUR_WEBHOOK_URL,
];

$request = new Request(
    'POST',
    API_BASE_URL . '/envelopes',
    [
        'Authorization' => 'Bearer ' . YOUR_API_KEY,
    ],
    new MultipartStream([
        [
            'name' => 'file',
            'contents' => stream_for(fopen('./example-document.pdf', 'r')),
        ],
        [
            'name' => 'options',
            'contents' => stream_for(json_encode($options)),
        ],
    ])
);

$client = new Client();
$response = $client->send($request);
$json = json_decode($response->getBody());
$envelope_id = $json->envelope_id;
{% /tab %}
{% tab language="csharp" %}
using (var pdfFileContent = new StreamContent(
    new FileStream(
        "test.pdf",
        FileMode.Open,
        FileAccess.Read)))
{
    using (var optionsJsonContent = new StringContent(
        optionsJson,
        Encoding.UTF8))
    {
        MultipartFormDataContent multiPartContent = new MultipartFormDataContent
        {
            { pdfFileContent, "file", "test.pdf" },
            { optionsJsonContent, "options" }
        };

        using (HttpRequestMessage request = new HttpRequestMessage
        {
            Method = HttpMethod.Post,
            RequestUri = new Uri("https://api.yotisign.com/v2/envelopes"),
            Content = multiPartContent
        })
        {
            request.Headers.Add("Authorization", "Bearer " + yotiAuthenticationToken);

            using (HttpClient httpClient = new HttpClient())
            {
                HttpResponseMessage response = httpClient.SendAsync(request).Result;
            }
        }
    }
}
{% /tab %}
{% tab language="go" %}
options := `{}`

	payload := &bytes.Buffer{}
	writer := multipart.NewWriter(payload)
	_ = writer.WriteField("options", options)
	
	file, err := os.Open("path/to.pdf")
	defer file.Close()
	formFile, err := writer.CreateFormFile("file",filepath.Base("path/to.pdf"))
	_, err = io.Copy(formFile, file)
	err = writer.Close()
	
	req, err := http.NewRequest("POST", "<BASE_URL>/v2/envelopes", payload)
	req.Header.Add("Authorization", "Bearer <API_KEY>")
	req.Header.Add("Content-Type", "multipart/form-data")
	req.Header.Set("Content-Type", writer.FormDataContentType())
	
	client := &http.Client{}
	response, err := client.Do(req)

	if err != nil {
		fmt.Println(err)
	} else {
		result, _ := ioutil.ReadAll(response.Body)
	}
{% /tab %}
{% /code %}

### Expected response

On success Yoti returns a 202 and a JSON object in the following format:

{% code %}
{% tab language="json" %}
{
    "envelope_id": "<envelopeId>"
}
{% /tab %}
{% /code %}

This envelope ID will be used to view your the envelope status and retrieve the document. 

### Error codes

{% table %}
| Error code | Description | 
| ---- | ---- | 
| 400 | Bad Request, example: id provided not a UUID | 
| 401 | Unauthorised request, example: requesting the status on an envelope you are not authorised to view | 
| 403 | Forbidden, requesting user did not create the envelope | 
| 413 | The combined file sizes have exceeded the 15MB limit | 
| 422 | The number of files uploaded has exceeded the 20 file limit | 
{% /table %}