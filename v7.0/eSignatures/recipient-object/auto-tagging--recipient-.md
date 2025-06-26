---
type: page
title: Auto-tagging (recipient)
listed: true
slug: auto-tagging--recipient-
description: 
index_title: Auto-tagging (recipient)
hidden: 
keywords: 
tags: 
---

You can add a tag to your template document using our auto tagging feature by inserting an anchor into your document. An anchor is made of:

- A Role
- Recipient number
- Tag Type
- Required/Optional

{% table %}
| Anchor Type | Example | Description | 
| ---- | ---- | ---- | 
| Role | Signer `(S)` | Role of the recipient | 
| Recipient number | x`(1 to 30)` | Number of recipients. This must be a number from 1 to 30. | 
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

To use the auto tagging feature you will first have to enable this in your options object. You will need to set the Industry Type based on the Signer Roles you wish to use. Please see the table below.

{% badge type="info" text="Hint" /%} You will have to leave the tags property in your recipients object. This can be empty.

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

A list of the roles the Yoti Sign API offers:

{% table %}
| Roles | Tag | Industry Type | 
| ---- | ---- | ---- | 
| Signer | S | GENERAL | 
| Tenant | T | REAL_ESTATE | 
| Landlord | L | REAL_ESTATE | 
| Agent | A | REAL_ESTATE | 
| Guarantor | G | REAL_ESTATE | 
{% /table %}

A list of the tag types the Yoti Sign API offers:

{% table %}
| Tag Types | Tag | Example | 
| ---- | ---- | ---- | 
| Signature | S | S1SR | 
| Text Field | T | S1TR | 
| Check Box | CB | S1CBR | 
| Date Signed | DS | S1DSR | 
| Radio Group | RG[X]* | S1RG1R | 
| Attachment | A | S1AR | 
{% /table %}

{% html %}
<div class="alert-GTK">
    <div class="alert-title" id="GTK">
        Good to know
    </div>
    <div class="alert-text">
        Make sure that your tags are formatted correctly by viewing the auto tagging matrix.

    </div>
    <div class="alert-links"> 
        <a href="https://www.yoti.com/wp-content/uploads/Sign_Auto-tagging-matrix.pdf">View matrix</a>
   </div>
</div>
{% /html %}