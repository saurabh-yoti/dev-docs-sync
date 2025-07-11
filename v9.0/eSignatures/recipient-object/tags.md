---
type: page
title: Tags
listed: true
slug: tags
description: 
index_title: Tags
hidden: 
keywords: 
tags: 
---

A tag is an array of objects used to place signature fields on a given document as shown below. There is a limit of 200 tags per recipient. A recipient can have 0 tags.

Yoti allows more than just signature fields so you can request more information on a document.

{% code %}
{% tab language="json" %}
"tags": [
                {
                    "page_number": 1,
                    "x": 0.1,
                    "y": 0.1,
                    "type": "signature",
                    "optional": false,
                    "file_name": "myfile.pdf"
                    "name": "sign-here",
                },
                {
                    "page_number": 1,
                    "x": 0.1,
                    "y": 0.1,
                    "type": "text_field",
                    "optional": false,
                    "file_name": "myfile.pdf"
                    "name": "signee-name",
                    "prefilled_value": "prefilled text",
                    "help_text": "help text"
                    "readonly": true,
                    "validation": {
                      "regex": "^[0-9]*$",
                      "error_message": "Numbers only",
                      "flags": "gm"
                    }
                }
            ],
{% /tab %}
{% /code %}

To populate a tag, you will need to specify a page number, x and y co-ordinate, and a tag type.

---

### Page number

This marks the page number of the page to place a tag.

{% code %}
{% tab language="json" %}
"tags": [

                {
                    "page_number": 1,
                }
            ],
{% /tab %}
{% /code %}

- This must correspond to a page number on the file designated by the **file_name** provided for the tag.
- If it does not match the envelope will not be created, and if subscribed an “upload_error” webhook will be sent.

---

### Width

This is is only applied to “text_field” tags.

{% code %}
{% tab language="json" %}
"tags": [
                {
                    "page_number": 1,
                    "x": 0.1,
                    "y": 0.1,
                    "width": 1,
                    "type": "text_field",
                    "optional": false,
                    "file_name": "myfile.pdf"
                    "name": "signee-name",
                    "prefilled_value": "prefilled text",
                    "readonly": true
                }
            ],
{% /tab %}
{% /code %}

- Its value must be greater than 0
- It is ignored for “signature” and “checkbox_field” tag types
- If the tag is a “text_field”**,** then the **width** + **x** must be less than 1.

---

### X

The 'X' co-ordinate of the tag field.

{% code %}
{% tab language="json" %}
"tags": [
                {
                    "x": 0.1,
                },

            ],
{% /tab %}
{% /code %}

- This is a decimal fraction of the page width.
- Minimum value can be 0 and maximum of 0.949.
- If the tag is a “text_field”**,** then the **width** + **x** must be less than 1.

---

### Y

{% code %}
{% tab language="json" %}
"tags": [
                {
                    "y": 0.1,
                },

            ],
{% /tab %}
{% /code %}

The 'Y' co-ordinate of the tag field,

- This is a decimal fraction of the page height.
- Minimum value can be 0 and maximum of 0.949.

---

### Type

This is the type of buttons / additional properties you can add on your document. 

{% code %}
{% tab language="json" %}
"tags": [
                {
                    "type": "signature",
                }

            ],
{% /tab %}
{% /code %}

This should be set to either:

{% table widths="" %}
| Type | Description | 
| ---- | ---- | 
| text_field | This allows a recipient to enter free text, a width value must be specified alongside "text_field" to define the size of the field. Width is only applied to "text field" and must be greater than 0. | 
| signature | This is used to indicate a click to sign box. | 
| checkbox_field | This is used to generate a check box for the user to select. | 
| radio_field | This is set to generate a radio button for the user to select. Multiple "radio_field" tags can be grouped using "tag group_name". | 
| initials | This allows a recipient to enter their initials. They have the option to enter free text, upload an image, or draw their initials. | 
| date_signed_field | If selected is auto generated by the Yoti Sign API to apply the date of when the signer submitted their signature to the document, in the position that a sender sets up during the sender flow. This is in UTC format and is not a manual input field. "optional" must be set to false if this field is configured. | 
| attachment | When a signer clicks on an attachment tag, they are prompted to upload a PDF. Only PDF files are currently supported. Once the envelope is completed, any attachments a signer has submitted can be found in the completion pack, which can be accessed using the `GET envelopes/:id/completed-documents` endpoint. | 
{% /table %}

---

### Optional

A tag can be marked as "optional" by adding the "optional" parameter.

{% code %}
{% tab language="json" %}
"tags": [
                {
                    "optional": false,
                }
            ],
{% /tab %}
{% /code %}

- If a tag is marked as "optional" a recipient will be allowed to sign the document without submitting the tag.
- If an "optional" tag is not submitted by a sender, the tag will not show up on the completed document.
- `yoti_attributes` may not be marked as "optional".

---

### Filename

The name of the document to be signed and must correspond to a filename of one of the files provided in the request (including the file extension).

{% code %}
{% tab language="json" %}
"tags": [
                {
                    "file_name": "myfile.pdf"
                }
            ],
{% /tab %}
{% /code %}

- The character limit is 255.
- If it does not match, the envelope will not be created and if subscribed an “upload_error” webhook will be sent.

---

### Name

A unique name attributed to the tag itself. 

- Is optional.
- Is unique for each tag for each recipient.
- Must be 50 characters or less.

---

### tag_group_name

Used to group multiple tags of the same type. If a tag group name is assigned there must be at least two tags with the same group name. These tags are linked together. This is to link tags together via this group name, therefore conditional logic rules can be applied to the whole tag group instead of a singular tag.

- Grouping radio fields by a tag group ensures only one radio field can be selected out of the group
- Tag groups must each have a minimum of 2 tags in them.
- Must not have both optional and required tags in the same tag group
- Must contain at least one alphanumeric character for tag_group_name (can only contain letters, digits & spaces.
- Must be 50 characters or less

---

### disable_resize

This property is only applicable to type text_field and prevents the field from expanding by locking it to a specific size. This is a boolean.

If not set, the signee can continue typing until the end of the document.

---

### prefilled_value

This is only applied to “text_field” tags. It is an optional property and must not contain any special characters. This will pre-fill the tag with the assigned string. This must not contain special characters: `/\:*?<>|`

{% code %}
{% tab language="json" %}
"tags": [
                {
                    "prefilled_value": "prefilled text",
                }
            ],
{% /tab %}
{% /code %}

---

### help_text

This is only applied to "text_field" tags. It is an optional property, must not contain any special characters and must also contain 255 characters or less. The help text will generate placeholder text in the input field. This must not contain special characters: `/\:*?<>|`

{% code %}
{% tab language="json" %}
"tags": [
                {
                    "help_text": "help text",
                }
            ],
{% /tab %}
{% /code %}

---

### readonly

This is only applied to “text_field” tags and it is an optional property. 

{% code %}
{% tab language="json" %}
"tags": [
                {
                    "readonly": true
                }
            ],
{% /tab %}
{% /code %}

This is a boolean which if set to true prevents a pre-filled value from being changed by the signer.

---

### validation

This is only applied to “text_field” tags and it is an optional property. Validation can be applied to text field tags so that signers must type out their response in the correct format. 

{% code %}
{% tab language="json" %}
"tags": [
                {
                    "validation": {
                      "regex": "^[0-9]*$",
                      "error_message": "Numbers only",
                      "flags": "gm"
                    }
                }
            ],
{% /tab %}
{% /code %}

{% table widths="168" %}
| Field | Description | 
| ---- | ---- | 
| regex | Desired text format for user to enter. Must be a valid regular expression e.g "^[0-9]*$" | 
| error_message | This is an error string which will be shown to the signer if their input fails the regex matching | 
| flags | You can enhance your regex matching with  any valid regex flags, in most cases the gm flag should be used. | 
{% /table %}

---

### merge fields

This can only be applied when the auth is set to "idv". We take the data extracted from the ID document and automatically place it into a tag field.

{% code %}
{% tab language="json" %}
"tags": [
                {
                    "merge_field": { 
                      "source": "idv",
                      "id_doc": 1,
                      "field_name": "full_name" 
                    },
                }
            ],
{% /tab %}
{% /code %}

{% table widths="" %}
| Field | Description | 
| ---- | ---- | 
| source | The source of the data, will always be "idv". | 
| id_doc | This determines which id document to get the data from. | 
| field_name | The data extraction field used to populate the tag, must match what the Yoti IDV API returns in the data extraction JSON. | 
{% /table %}

{% callout type="error" title="Important" %}
merge fields can not be used when a OTP is enabled.
{% /callout %}