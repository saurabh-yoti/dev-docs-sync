---
type: page
title: IDV object
listed: true
slug: idv-object
description: 
index_title: IDV object
hidden: 
keywords: 
tags: 
---

This is where you can specify an identity verification check to be completed alongside the signing of documents. This makes use of our identity verification service, more details regarding this can be found [here](https://developers.yoti.com/identity-verification/overview). You will need to specify the configuration for the types of checks that you need, we have predefined configurations but you also have the option to create and use a custom configuration.

{% code %}
{% tab language="json" %}
"verification":
            {
                "idv":
                {
                    "session_config_name": "Real Estate",
                    "when": "before_viewing",
                    "session_limit": 10,
                    "blocks_signing": ["deadend_errors", "merge_field_not_resolved"]
                }
            }
{% /tab %}
{% tab language="json" title="JSON - AGE" %}
"verification":
            {
                "age": {
                  "age_estimation": {
                    "allowed": true
                   }
                }
            }
{% /tab %}
{% /code %}

---

#### Session_config_name

The name of either a prebuilt configuration or a customised configuration.

{% code %}
{% tab language="json" %}
"session_config_name": "Real Estate"
{% /tab %}
{% /code %}

{% table widths="212" %}
| Session_config_name | Description | 
| ---- | ---- | 
| Real Estate | Prebuilt session configuration, the json can be found [here](https://developers.yoti.com/eSignatures/json-examples#real-estate). | 
| HR | Prebuilt session configuration, the json can be found [here](https://developers.yoti.com/eSignatures/json-examples#hr). | 
| Finance | Prebuilt session configuration, the json can be found [here](https://developers.yoti.com/eSignatures/json-examples#finance). | 
| Adult | Prebuilt session configuration, the json can be found [here](https://developers.yoti.com/eSignatures/json-examples#adult). | 
| Recruitment | Prebuilt session configuration, the json can be found [here](https://developers.yoti.com/eSignatures/json-examples#recruitment). | 
| Liveness Only | Prebuilt session configuration, the json can be found [here](https://developers.yoti.com/eSignatures/json-examples#liveness-only). | 
| Custom* | A custom configuration that can be created and then named by you. | 
{% /table %}

---

#### When

Specifies when the identity verification should take place

{% badge type="info" text="Hint" /%} currently the only option is "before_viewing"

{% code %}
{% tab language="json" %}
"when": "before_viewing"
{% /tab %}
{% /code %}

{% table widths="" %}
| When | Description | 
| ---- | ---- | 
| before_viewing | Identity verification will take place before the signing process. | 
| after_submitting | The document signing itself will complete independently of the verification. Once the user has signed, the signer can return to the signing link to complete the Id verification at another time. Once they have submitted a verification session they will not be able to return to the signing link | 
{% /table %}

---

#### session_limit

This represents the maximum number of identity verification sessions that can be created by a recipient. 

- The minimum limit is 1.
- The maximum limit is 10

---

#### blocks_signing 

This represents the ability to block the user from signing the document if any errors occur in the identity verification process.

{% table widths="" %}
| Attribute | Description | 
| ---- | ---- | 
| deadend_errors | The signer will not be able see/sign the document if any errors occur in the identity verification process. | 
| merge_field_not_resolved | The signer will not be able see/sign the document if the merge field configured in your tags array is not pre-populated. | 
{% /table %}