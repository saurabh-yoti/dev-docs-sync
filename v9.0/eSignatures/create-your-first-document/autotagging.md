---
type: page
title: Autotagging
listed: true
slug: autotagging
description: 
index_title: Autotagging
hidden: 
keywords: 
tags: 
---

{% html %}
<div class="alert-GTK">
    <div class="alert-title" id="GTK">
        Good to know
    </div>
    <div class="alert-text">
       The autotagging feature is available upon request.
    </div>
    <div class="alert-links"> 
        <a href="https://support.yoti.com/yotisupport/s/contactsupport">Contact us</a>
   </div>
</div>
{% /html %}

{% html %}
<div class="alert-BYS">
   <div class="alert-title" id="BYS">
      Before you start
   </div>
   <div class="alert-text" >
You will need to have added a document to the portal.   </div>
   <div class="alert-links"> 
   </div>
</div>
{% /html %}

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

A list of the roles the Yoti Sign API offers:

{% table %}
| Roles | Tags | 
| ---- | ---- | 
| Signer | S | 
| Tenant | T | 
| Landlord | L | 
| Agent | A | 
| Guarantor | G | 
| Contractor | C | 
{% /table %}

A list of the tag types the Yoti Sign API offers:

{% table %}
| Tag Types | Tag | Example | 
| ---- | ---- | ---- | 
| Signature | S | &#124;S1SR&#124; | 
| Text Field | T | &#124;S1TR&#124; | 
| Check Box | CB | &#124;S1CBR&#124; | 
| Date Signed | DS | &#124;S1DSR&#124; | 
| Radio Group | RG[X]* | &#124;S1RG1R&#124; | 
| Attachment | A | &#124;S1AR&#124; | 
| Initials | IN | &#124;S1INR&#124; | 
{% /table %}

A list of the metadata tags the Yoti Sign API offers:

{% table %}
| MetaTag Type | MetaTag | Example | 
| ---- | ---- | ---- | 
| Name | nm | &#124;S1TR{"nm":"my name value"}&#124; | 
| Prefill | ph | &#124;S1TR{"ph":"my placeholder value"}&#124; | 
| Placeholder | pf | &#124;S1TR{"pf":"my prefill value"}&#124; | 
{% /table %}

Note the metadata tag types can only be used for the Text field(TR) tag type.

Auto-tagging allows you to dynamically tag a document by including special anchor tags inside the document itself.

- Click **Options** and **Auto-tagging.**

{% image url="https://image-archive.developerhub.io/image/upload/v2_2762/xhxgyatyb1kakitxe5vl/1615987329.png" caption="Options &gt; Auto-tagging" mode="responsive" height="680" width="1932" %}
{% /image %}

- Press **apply**.

{% image url="https://image-archive.developerhub.io/image/upload/v2_2762/vureknbhass0galsrke0/1615987389.png" caption="Options &gt; Auto-tagging &gt; Apply fields" mode="300" height="728" width="930" %}
{% /image %}

- Now you can press **NEXT** and continue with the document set up.