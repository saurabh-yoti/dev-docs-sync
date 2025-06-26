---
type: page
title: Address check
listed: true
slug: address-check
description: 
index_title: Address check
hidden: 
keywords: 
tags: 
---

It is possible to extend the Identity verification integration by requesting an address check as part of a session.

{% html %}
<div class="alert-BYS">
   <div class="alert-title" id="BYS">
      Before you start
   </div>
   <div class="alert-text" >
Please read through our document check section   </div>
   <div class="alert-links"> 
         <a target="_self" href="https://developers.yoti.com/identity-verification/document-checking">Document check</a>
   </div>
</div>
{% /html %}

{% html %}
<div class="alert-GTK">
    <div class="alert-title" id="GTK">
        Good to know
    </div>
    <div class="alert-text">
Yoti recommends that you inform your users that their data might be checked against a third party data source as part of the identity check.    </div>
    <div class="alert-links"> 

   </div>
</div>
{% /html %}

This check will facilitate an extra verification of a user by searching a person’s details against a collated database from various sources worldwide.

Yoti will need to capture the user's address so you will need to allow the following checks:

{% table widths="247,0,0" %}
| Name | Resources | Type | Manual check available | 
| ---- | ---- | ---- | ---- | 
| Supplementary text data extraction | 1x Document Resource | Asynchronous | ✅ | 
| ID document text data extraction | 1x Document Resource | Asynchronous | ✅ | 
{% /table %}

A **successful** text data extraction of the name, address and date of birth. If we are unable to extract the data the check will not be performed.

{% badge type="success" text="Hint: " /%} If an address is extracted from both an ID document and supporting document, the supporting document address is used for the check. You may want to look at our document settings section to filter out specific documents in [auto$](/identity-verification/document-checking). 

If you decide to ask for two documents, both the primary and secondary ID document will be sourced for attributes required to complete the check. If a supporting document is supplied, the address from that will be used, otherwise we’ll use the one from primary or secondary ID document.

To request this check, a `thirdpartyidentitycheck` must be specified.

{% code %}
{% tab language="javascript" %}
const thirdPartyIdentityCheck = new RequestedThirdPartyIdentityCheckBuilder()
   .build();

const sessionSpec = new SessionSpecificationBuilder()
    // ...
    .withRequestedCheck(thirdPartyIdentityCheck)
    // ...
    .build();
{% /tab %}
{% tab language="java" %}
RequestedThirdPartyIdentityCheck thirdPartyIdentityCheck = RequestedThirdPartyIdentityCheck.builder().build();

SessionSpec sessionSpec = SessionSpec.builder()
        // ...
        .withRequestedCheck(thirdPartyIdentityCheck)
        // ...
        .build();
{% /tab %}
{% tab language="php" %}
// COMING SOON
{% /tab %}
{% tab language="python" %}
# COMING SOON
{% /tab %}
{% tab language="csharp" %}
// COMING SOON
{% /tab %}
{% tab language="go" %}
// COMING SOON
{% /tab %}
{% tab language="java" title="Java v2" %}
RequestedThirdPartyIdentityCheck thirdPartyIdentityCheck = RequestedCheckBuilderFactory.newInstance().forThirdPartyIdentityCheck().build();

SessionSpec sessionSpec = SessionSpecBuilderFactory.newInstance().create()
        // ...
        .withRequestedCheck(thirdPartyIdentityCheck)
        // ...
        .build();
{% /tab %}
{% /code %}

{% badge type="success" text="Hint: " /%} To ensure the check can consistently be performed, we recommend creating a session that asks for one ID document, and one supporting proof of address document.

{% html %}
<div class="alert-GTK">
    <div class="alert-title" id="GTK">
       Jump to.. 
    </div>
    <div class="alert-text">
       On successful completion, the check outputs a report  which can be found in the ‘retrieve results’ section.
      Details of the report can be found in 'Understanding the report' section.
      
     
    </div>
    <div class="alert-links"> 
        <a href="https://developers.yoti.com/identity-verification/results#document-settings">Retrieve results</a>
        <a target="_self" href="https://developers.yoti.com/identity-verification/address-report">Understanding the report</a> 
   </div>
</div>
{% /html %}