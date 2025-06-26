---
type: page
title: Recipient object
listed: true
slug: embedded-recipient-object
description: 
index_title: Recipient object
hidden: 
keywords: 
tags: 
---

Here is where you will need to provide an array of JSON objects to define the intended recipient of the document. This array can hold up to **10** recipients and 10 non signer recipients. 

{% code %}
{% tab language="json" %}
{

    "recipients": [
        {
            "type": "SIGNER",
            "name": "User 1",
            "email": "user1@gtest.com",
            "role": "Signee",
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
            ],
            "iso_country_code": "GB",
            "mobile_number": "7999999999",
            "witness": {
              "tags": [
                ...
              ]
            }
        }
        "event_notifications": []
    ]
}
{% /tab %}
{% /code %}

{% table widths="149" %}
| Parameter | Description | 
| ---- | ---- | 
| Type | Type of signer: SIGNER or CC. For more information on CC see below.\n\nSigner: User to sign and receive confirmation email.\n\nCC: User to receive the confirmation on signing automatically without signing. | 
| name | This should be a string and should not be less than 1 character with a maximum length of 100 characters. The name specifies the name of the target recipient. | 
| email | The email specifies the email address of the target recipient. This must be a valid email address (RFC 5322). | 
| role | String value of role of the recipient, this is free text and can be used to identify the role of the recipient, the maximum length is 50 characters. | 
| auth_type | Auth_type can be one of either\n\n\n\n- "no-auth": A digital signature is required.\n- "sign-auth": A Yoti scan will be required for this signature.\n\n\nThe email_address attribute is added by default to the list of Yoti attributes even if no attributes are provided.\n\n\n\nIf you select sign-auth the list of Yoti attributes that can be used are:\n\n\n- full_name\n- email_address - This is enabled by default,\n- date_of_birth,\n- postal_address,\n- gender,\n- nationality,\n- phone_number,\n- photo, - This is a photo of the user\n- photo_auth. - This is to prompt the user to take a selfie of themselves live via the Yoti App as extra level of security. | 
| sign_group | This defines an order in which recipients receive invitations to sign a document. For example, all recipients within sign group 1 will be the first to receive a document to sign. Once all recipients from sign group 1 have signed, the document will be sent to sign group 2. There must be at least 1 sign_group, and the order must be sequential, starting from 1.\n\n\nWith embedded signing, the signing group can also be controlled by choosing when to render a specific embedded envelope by token id. | 
| Country code | If the `has_envelope_otps` is toggled true, Yoti will return a country code in a valid two letter ISO country code format. | 
| Phone number | If the `has_envelope_otps` is toggled true, Yoti will return a valid mobile number. \n\n\n\n{% badge type="success" text="Hint" /%} Please ensure the correct country code is used and remove the first digit of the mobile number. | 
| event_notifications | This property must be present for embedded envelopes. An empty array means that event notifications will not be sent.\n\nAccepted notifications are `signer_invitation` or `envelope_completion` | 
{% /table %}

### Add a non signing recipient

You can add an email address to the recipient object that the sender creates so that a non signing recipient receives a copy of the completion pack. The non signing recipient (CC recipient) does not receive an invitation to the envelope while it is in an incomplete state. 

Once the envelope is complete and all signers have signed then the completion pack email is triggered and are sent to all recipients including non signing recipients.

{% code %}
{% tab language="json" %}
"recipients": [
        {
            "type": "SIGNER",
            "name": "User 1",
            "email": "user1@gtest.com",
            "role": "Signee",
            "auth_type": "no-auth", 
            "sign_group": 1,
            "country_code": "GB",
            "phone_number": "7999999999",
        },
        {
          "type": "CC",
          "name": "CC Recipient",
          "email": "cc-recipient@test.com"
        }
          "event_notifications": []
    ],
{% /tab %}
{% /code %}

{% table %}
| Parameter | Description | 
| ---- | ---- | 
| Type | Type of signer, in this case CC. | 
| Name | Name of the receipt you want to CC. | 
| Email | Email of the recipient to be CC'd | 
{% /table %}

---

## Tags explained

A tag is an array of objects used to place signature fields on a given document as shown below.  There is a limit of 200 tags per recipient. A recipient can have 0 tags.

{% code %}
{% tab language="json" %}
{
"tags": [
                {
                    "page_number": 1,
                    "x": 0.1,
                    "y": 0.1,
                    "type": "signature",
                    "optional": false,
                    "file_name": "myfile.pdf"
                }
            ],

}
{% /tab %}
{% /code %}

To populate a tag, you will need to specify a page number, x and y co-ordinate, and a tag type.

{% table %}
| Parameter | Description | 
| ---- | ---- | 
| page_number | This marks the page number of the page to place a tag. \n\n\n\n- This must correspond to a page number on the file designated by the **file_name** provided for the tag.\n- If it does not match the envelope will not be created, and if subscribed an “upload_error” webhook will be sent. | 
| width | This is is only applied to “text_field” tags.\n\n\n\n- Its value must be greater than 0\n- It is ignored for “signature” and “checkbox_field” tag types\n- If the tag is a “text_field”**,** then the **width** + **x** must be less than 1. | 
| x | The 'X' co-ordinate of the tag field.\n\n\n- This is a decimal fraction of the page width. \n- Minimum value can be 0 and maximum of 0.949.\n- If the tag is a “text_field”**,** then the **width** + **x** must be less than 1. | 
| y | The 'Y' co-ordinate of the tag field, \n\n\n- This is a decimal fraction of the page height. \n- Minimum value can be 0 and maximum of 0.949. | 
| type | This should be set to either:\n\n\n\n- Text_field - allows a recipient to enter free text, a width value must be specified alongside "text field" to define the size of the field. Width is only applied to "text_field" and must be greater than 0.\n- Signature - used to indicate a click to sign box.\n- Checkbox_field- used to generate a check box for the user to select.\n- Radio_field - sed to generate a radio button for the user to select. For multiple "radio_fields", these can be grouped using "tag_group_name".\n- date_signed_field - if selected is auto generated by the Yoti Sign API to apply the date of when the signer submitted their signature to the document, in the position that a sender sets up during the sender flow. This is in UTC format and is not a manual input field. optional must be set to false if this field is configured. | 
| optional | A tag can be marked as "optional" by adding the "optional" parameter. \n\n\n\n- If a tag is marked as "optional" a recipient will be allowed to sign the document without submitting the tag. \n- If an "optional" tag is not submitted by a sender, the tag will not show up on the completed document. | 
| filename | The name of the document to be signed and must correspond to a filename of one of the files provided in the request (including the file extension). \n\n\n\n- The character limit is 255.\n- If it does not match, the envelope will not be created and if subscribed an “upload_error” webhook will be sent. | 
| tag_group_name | Used to group multiple tags of the same type. \n\n\n\n- Grouping radio fields by a tag group ensures only one radio field can be selected out of the group\n- Tag groups must each have a minimum of 2 tags in them.\n- Must not have both optional and required tags in the same tag group\n- Must contain at least one alphanumeric character for tag_group_name (can only contain letters, digits & spaces.\n- Must be 50 characters or less | 
| disable_resize | This property is only applicable to type text_field and prevents the field from expanding by locking it to a specific size. This is a boolean.\n\n\n\nIf not set, the signee can continue typing until the end of the document. | 
{% /table %}

### Auto-tagging

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

{% badge type="info" text="Hint" /%} If using roles other than Signer, the "autotagging" parameter should be set to "REAL_ESTATE".

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

A list of the tag types  the Yoti Sign API offers:

{% table %}
| Tag Types | Tag | Example | 
| ---- | ---- | ---- | 
| Signature | S | S1SR | 
| Text Field | T | S1TR | 
| Check Box | CB | S1CBR | 
| Date Signed | DS | S1DSR | 
| Radio Group | RG[X]* | S1RG1R | 
{% /table %}

{% html %}
<div class="alert-GTK">
    <div class="alert-title" id="GTK">
        Good to know
    </div>
    <div class="alert-text">
        Make sure that your tags are formatted correctly by viewing the auto tagging matrix's.

    </div>
    <div class="alert-links"> 
        <a href="https://www.yoti.com/wp-content/uploads/Sign_Auto-tagging-matrix.pdf">View matrix</a>
        <a href="https://www.yoti.com/wp-content/uploads/Sign_real-estate-autotagging-matrix.pdf">View real estate matrix</a>
   </div>
</div>
{% /html %}

## Witness

When creating an envelope, you can specify that a recipient needs a witness. Witness details are defined by the signer when they sign the envelope, by providing the email address and name of the witness. The witness will sign to assert that they have witnessed the recipient signer signing the envelope. You can also assign document tags to the witness, in the same way that they can do so for the signer. 

When the recipient signer has successfully completed their signing, the witness is then sent an email asking them to confirm that they have witnessed the signing. 

{% code %}
{% tab language="json" %}
{

            "witness": {
              "tags": [
                ...
              ]
}
{% /tab %}
{% /code %}

{% table %}
| Parameter | Description | 
| ---- | ---- | 
| Witness | Yoti requires at least one tag for a witness. | 
| Tags | See above | 
{% /table %}