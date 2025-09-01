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

Here is where you will need to provide an array of JSON objects to define the intended recipient of the document. This array can hold up to **30** recipients and 30 non signer recipients. 

{% badge type="info" text="Hint" /%} For embedded envelopes recipient signers and witnesses can be assigned tags but they are not required. To assign a witness with no tags to a signer, add "witness": {} to the recipient JSON object.

{% code %}
{% tab language="json" title="No auth" %}
{
    "recipients": [
        {
            "type": "SIGNER",
            "name": "User 1",
            "email": "user1@gtest.com",
            "role": "Signee",
            "auth_type": "no-auth",
            "sign_group": 1,
            "active_for_seconds": 86400,
            "time_zone_name": "Pacific/Auckland",
            "event_notifications": ["signer_invitation", "envelope_completion"],
            "excluded_files": ["myfile2.pdf"],
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
            "mobile_number": 7999999999,
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
{% tab language="json" title="IDV auth" %}
// With IDV
{
    "recipients": [
        {
            "type": "SIGNER",
            "name": "User 1",
            "email": "user1@gtest.com",
            "role": "Signee",
            "auth_type": "idv",
            "sign_group": 1,
            "time_zone_name": "Pacific/Auckland",
            "event_notifications": ["signer_invitation", "envelope_completion"],
            "excluded_files": ["myfile2.pdf"],
            "verification":
             {
               "idv":
               {
                 "session_config_name": "Real Estate", 
                 "when": "before_viewing",
                 "session_limit": 10
               }
             },
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
            "mobile_number": 7999999999,
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

---

### Type

This is type of signer.

{% code %}
{% tab language="json" %}
"type": "SIGNER",
{% /tab %}
{% /code %}

{% table %}
| Type | Description | 
| ---- | ---- | 
| SIGNER | User to sign and receive confirmation email. | 
| CC | User to receive the confirmation on signing automatically without signing. \n\n\n\n- CC recipients can only have the `name` and `email` fields.\n- CC recipients receive the same completion pack as the sender, but do not sign the envelope.\n- CC recipients can be signers and / or witnesses, but the email address must be unique in the pool of CC recipients in the envelope.\n- There can be a maximum of 30 `CC` recipients, and 30 `SIGNER` recipients.\n- The number of `CC` recipients does not impact the limit on `SIGNER` recipients and visa versa. | 
{% /table %}

---

### Name

This is the name of the signer. 

{% code %}
{% tab language="json" %}
"name": "User 1",
{% /tab %}
{% /code %}

- This must be between 1 and 100 characters.
- This must not contain special characters: `/\:*?<>|`

---

### Email

The email specifies the email address of the target recipient. This must be a valid email address (RFC 5322).

{% code %}
{% tab language="json" %}
"email": "user1@gtest.com",
{% /tab %}
{% /code %}

---

### Roles

This is a string value of role of the recipient, this is free text and can be used to identify the role of the recipient, the maximum length is 50 characters. This must not contain special characters: `/\:*?<>|`

{% code %}
{% tab language="json" %}
"role": "Signee",
{% /tab %}
{% /code %}

---

### Auth type

This is the level of authorisation you want to set per envelope. 

{% code %}
{% tab language="json" %}
"auth_type": "no-auth", //sign-auth // idv
{% /tab %}
{% /code %}

{% table %}
| Auth type | Description | 
| ---- | ---- | 
| no-auth | A digital signature is required. | 
| sign-auth | A Yoti scan will be required for this signature.\n\nThe email_address attribute is added by default to the list of Yoti attributes even if no attributes are provided. | 
| idv | An identity verification session will be required for this envelope. More details can be found [here](https://developers.yoti.com/eSignatures/idv-object). | 
{% /table %}

If you select sign-auth the the email_address attribute will always be used and a list of additional Yoti attributes that can be used are:

- full_name
- date_of_birth,
- postal_address,
- gender,
- nationality,
- phone_number,
- photo, - This is a photo of the user
- photo_auth. - This is to prompt the user to take a selfie of themselves live via the Yoti App as extra level of security.

Example shown below for `sign-auth`:

{% code %}
{% tab language="json" %}
{
    "recipients": [
        {
            "type": "SIGNER",
            "name": "User 1",
            "email": "user1@gtest.com",
            "role": "Signee",
            "auth_type": "sign-auth",
            "yoti_attributes": [
                "full_name",
                "postal_address",
                "photo",
                "gender",
                "nationality",
                "date_of_birth"
         ],
            "sign_group": 1,
            "tags": [
              ...
            ],
            "iso_country_code": "GB",
            "mobile_number": "7999999999",

        }
    ]
}
{% /tab %}
{% /code %}

---

### Sign group

This defines an order in which recipients receive invitations to sign a document. For example, all recipients within sign group 1 will be the first to receive a document to sign. Once all recipients from sign group 1 have signed, the document will be sent to sign group 2. There must be at least 1 sign_group, and the order must be sequential, starting from 1.

{% badge type="info" text="Hint" /%} Through embedded signing, any required signing order should be controlled entirely by the integrator. It is recommended to utilise webhook notifications to understand when recipients have signed.

{% code %}
{% tab language="json" %}
{
   "name": "Test name",
   "emails": {
      "invitation": {
         "body": {
            "message": "test"
         }
      },
      "reminders": {
         "frequency": 2
      }
   },
   "recipients": [
      {
         "name": "Test name",
         "type": "SIGNER",
         "email": "test@yoti.com",
         "role": "Tester",
         "auth_type": "no-auth",
         "witness": {
            "auth_type": "sign-auth",
            "tags": [
               {
                  "page_number": 1,
                  "x": 0.15,
                  "y": 0.1,
                  "type": "signature",
                  "optional": false,
                  "file_name": "sample.pdf"
               }
        
            ]
         },
         "sign_group": 2,
         "tags": [
            {
               "page_number": 1,
               "x": 0.3,
               "y": 0.2,
               "type": "text_field",
               "optional": false,
               "file_name": "sample.pdf",
               "disable_resize": false,
               "width": 0.4
            }
         ]
      }
   ],
   "notifications": {
      "destination": "https://hookb.in/8PP6NP7lgjfBWWYjnnLO",
      "subscriptions": []
   }
}
{% /tab %}
{% /code %}

{% badge type="custom" text="Note" /%} A witness cannot have sign-auth and any such configuration is ignored.

---

### Active for seconds

The active for seconds field is a numeric value in seconds, with the Max being 1 year. It tells us how long to keep the signer’s recipient token active for and can be configured per signer. The default value is 2 days, and when the period expires, the signer will have to go through additional security measure e.g confirming their email address/mobile number before they can see the documents.

{% code %}
{% tab language="json" %}
"active_for_seconds": 86400,
{% /tab %}
{% /code %}

{% badge type="custom" text="Note" /%} For embedded envelopes this self-reactivation will not be possible, due to security reasons. The integrator will have to manually extend those tokens using the new endpoint - [here](https://developers.yoti.com/eSignatures/extend-recipient-tokens).

---

### Time zone name

This will effect the date signed field tag, with the relevant timezone. And Must be a **TZ database name.** This feature is available upon request.

{% code %}
{% tab language="json" %}
"time_zone_name": "Pacific/Auckland",
{% /tab %}
{% /code %}

---

### Event notifications

This defines the events that trigger email or sms notifications for the recipients. If the event names are included in the array, An email or sms will be sent for that event. If omitted for the standard envelope creation,  the signer invitation and envelope completion email notifications will be sent by default. If you include an sms notification, you must also include an email notification. An sms notification requires valid mobile_number and iso_country_code fields.

{% code %}
{% tab language="json" %}
"event_notifications": ["signer_invitation", "signer_invitation_sms", "envelope_completion"],
{% /tab %}
{% /code %}

{% table %}
| Event type | Description | Embedded | Non-embedded | 
| ---- | ---- | ---- | ---- | 
| signer_invitation | email notification is sent to the recipient, informing them to sign. | ✅ | ✅ | 
| signer_invitation_sms | text message is sent to the recipient, informing them to sign. | ❌ | ✅ | 
| envelope_completion | email notification is sent to the recipient, informing that everyone has signed the document. | ✅ | ✅ | 
{% /table %}

---

### Excluded files

The documents specified in this array will not appear for the user when they are directed to the signing page. The documents need to be valid documents that have been added to the envelope, and there can't be any tags on the excluded documents.

{% code %}
{% tab language="json" %}
"excluded_files": ["myfile2.pdf"]
{% /tab %}
{% /code %}

---

### Country code

If the `has_envelope_otps` is toggled true, Yoti will return a country code in a valid two letter ISO country code format.

{% code %}
{% tab language="json" %}
"iso_country_code": "GB",
{% /tab %}
{% /code %}

---

### Phone number

If the `has_envelope_otps i`s toggled true, Yoti will return a valid mobile number.

{% code %}
{% tab language="json" %}
"mobile_number": 7999999999,
{% /tab %}
{% /code %}

{% badge type="success" text="Hint" /%} Please ensure the correct country code is used and remove the first digit of the mobile number.

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