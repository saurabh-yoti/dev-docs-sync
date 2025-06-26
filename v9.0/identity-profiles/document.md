---
type: page
title: Document
listed: true
slug: document
description: 
index_title: Document
hidden: 
keywords: 
tags: 
---

If you wish to request a document from the user this section will provide you context on what this check entails. Yoti will provide a report of the result from the document check.

The user will have the option to upload an image or capture a photo of their document. This is configurable in your session creation via our API / SDK or Portal settings. Yoti recommends you have both options available.

This section will describe:

- What document checks are performed.
- How to enhance your document check.
- Outcome report with recovery suggestions.

Our hybrid approach uses both automatic and manual processes to check the security features of each unique ID document to make sure it’s genuine.

The below checks are related to document checks available at Yoti:

{% table widths="0,356,242" %}
| Name | Description | Resources | Manual check available | 
| ---- | ---- | ---- | ---- | 
| Document authenticity | A request to assess the characteristics of a document, to determine the validity of the ID document. Yoti will perform multiple checks on a ID document. | 1x Document Resource | ✅ | 
| Text extraction | A request to obtain the data printed visually on a document, in structured form. | 1x Document Resource | ✅ | 
{% /table %}

## Enhance your check

Add these features to enhance your check for a stronger verification.

{% table widths="0,0,242" %}
| Name | Description | Resources | Manual check available | 
| ---- | ---- | ---- | ---- | 
| Filters | Restriction of document types / countries. If you do not wish to accept all documents or countries you can configure your session to add / remove which countries and document types are displayed to the user on the user view. | N/A | N/A | 
| Supporting documents | Yoti offers the ability to request additional documents to enhance the verification of the user.\n\n\n\nSupporting documents:\n\n\n\n- Council Tax bill\n- Bank statement\n- Phone bill\n- Utility bill | 1x Document Resource | ✅ | 
| Document comparison | If you request your users to upload more than one document we offer the ability to cross check the data | 2x Document Resource | ❌ | 
| NFC | Enable Near Field Communication (NFC) for native integrations. | 1x Document Resource | ❌ | 
| Translations | Change the language of the information displayed to the end user. | N/A | N/A | 
{% /table %}

---

## User flow

1. The user will be presented with a drop down of countries and types of ID to pick from.  If you like you can preset which country is shown first, you can also remove countries and document types you do not want to support.

{% image url="https://uploads.developerhub.io/prod/kvAX/nqt4u5uqnha2xldar75jy7rozlc0wgyxzw697lp7jhscx0kims4o8canzuboc02i.png" caption="User flow: Add a document" mode="responsive" height="1204" width="1874" %}
{% /image %}

2. The user will take a photo of their ID or upload their ID. Yoti will predominately highlight taking a live capture over upload. You can remove the option to upload if you wish.

{% image url="https://uploads.developerhub.io/prod/kvAX/erbva0nqcx4y3lcnuap7w9mj5fli09mjubfs8h24w8um1fp3xm6g49md4l1g69j6.png" caption="User flow: Option to take photo or upload." mode="responsive" height="1204" width="1848" %}
{% /image %}

{% image url="https://uploads.developerhub.io/prod/kvAX/qexv89jlrzr804fujxprav20yccx26b6o5yxt1x8r1oom7wu1ij0z4tug73k9vkk.png" caption="User flow: Upload option." mode="responsive" height="1206" width="1864" %}
{% /image %}

Note: Some documents may ask for the front and the back of the document. If the document has been uploaded incorrectly we will trigger in session feedback to prompt the user to try and upload again.

{% image url="https://uploads.developerhub.io/prod/kvAX/2zugas7u6klnowvefm0wrspqnpttkc5599amv4n578vkx2cglk8etviki5ak5vxh.png" caption="User flow: In Session feedback" mode="responsive" height="1164" width="1868" %}
{% /image %}

The user will need to either Change the document or try again.

3. The user will be presented with a complete screen.

{% image url="https://uploads.developerhub.io/prod/kvAX/y3tqxby3v4ih4d3n882qvgyaq4xwybc6n5zteccrafvt1pf7jvrfwahcust5lczt.png" caption="User: End screen" mode="responsive" height="1208" width="1860" %}
{% /image %}

At this point you can redirect the user to a success URL / Error URL.