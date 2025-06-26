---
type: page
title: Recipient object
listed: true
slug: recipient-object
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
                    "file_name": "myfile.pdf",
                    "name": "signee-name"
                }
            ],
            "iso_country_code": "GB",
            "mobile_number": "7999999999",
            "witness": {
                "tags": [
                ...
                ]
            },
            "rules": [
                {
                    "action": "show",
                    "conditions": [
                        {
                            "trigger_tag_name": "sign-here",
                            "criteria": "has_value"
                        }
                    ],
                    "affected_tag_names": [
                        "signee-name"
                    ]
                }
            ]
        }
    ]
}
{% /tab %}
{% /code %}

{% table widths="105" %}
| Parameter | Description | 
| ---- | ---- | 
| Type | Type of signer: SIGNER or CC. For more information on CC see below.\n\nSigner: User to sign and receive confirmation email.\n\nCC: User to receive the confirmation on signing automatically without signing. | 
| name | This should be a string and should not be less than 1 character with a maximum length of 100 characters. The name specifies the name of the target recipient. | 
| email | The email specifies the email address of the target recipient. This must be a valid email address (RFC 5322). | 
| role | String value of role of the recipient, this is free text and can be used to identify the role of the recipient, the maximum length is 50 characters. | 
| auth_type | Auth_type can be one of either\n\n\n\n- "no-auth": A digital signature is required.\n- "sign-auth": A Yoti scan will be required for this signature.\n\n\nThe email_address attribute is added by default to the list of Yoti attributes even if no attributes are provided. | 
| yoti_attributes | If you select sign-auth the list of Yoti attributes that can be used are:\n\n\n- full_name\n- email_address - This is enabled by default,\n- date_of_birth,\n- postal_address,\n- gender,\n- nationality,\n- phone_number,\n- photo, - This is a photo of the user\n- photo_auth. - This is to prompt the user to take a selfie of themselves live via the Yoti App as extra level of security. | 
| sign_group | This defines an order in which recipients receive invitations to sign a document. For example, all recipients within sign group 1 will be the first to receive a document to sign. Once all recipients from sign group 1 have signed, the document will be sent to sign group 2. There must be at least 1 sign_group, and the order must be sequential, starting from 1. | 
| Country code | If the `has_envelope_otps` is toggled true, Yoti will return a country code in a valid two letter ISO country code format. | 
| Phone number | If the `has_envelope_otps i`s toggled true, Yoti will return a valid mobile number. \n\n\n\n{% badge type="success" text="Hint" /%} Please ensure the correct country code is used and remove the first digit of the mobile number. | 
| event_notifications | An empty array means that event notifications will not be sent. Accepted notifications are `signer_invitation` or `envelope_completion` | 
{% /table %}

---

## Add a non signing recipient

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