---
type: page
title: Aadhaar
listed: true
slug: aadhaar
description: 
index_title: Aadhaar
hidden: 
keywords: 
tags: 
---

Due to government restrictions Aadhaar numbers cannot be shared and it is mandatory to mask them. We return to businesses only masked images of Aadhaar cards. Unmasked images are deleted from our backend as soon as all checks are done.

Example of masking of front and back of card:

There are many different formats for Aadhaar cards with the number possibly on the front and/or back. We will check both the back and the front of the card and mask any identified Aadhaar number. If there is no number detected then you will not be able to retrieve the images. The retrieval request will return 204 NO_CONTENT.

{% image url="https://image-archive.developerhub.io/image/upload/23602/ourgxj9ze0zbe4mogr93/1585254605.jpg" caption="Aadhaar - Back" mode="300" height="762" width="1198" %}
{% /image %}

{% image url="https://image-archive.developerhub.io/image/upload/23602/kvkz5sfxemcuzst0djrp/1585254592.jpg" caption="Aadhaar - Front" mode="300" height="772" width="1228" %}
{% /image %}

Aadhaar resources will only become available when the masking has been completed.