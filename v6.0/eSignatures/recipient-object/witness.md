---
type: page
title: Witness
listed: true
slug: witness
description: 
index_title: Witness
hidden: 
keywords: 
tags: 
---

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
| Tags | See Auto-tagging section. | 
{% /table %}