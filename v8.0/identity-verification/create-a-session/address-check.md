---
type: page
title: Address
listed: true
slug: address-check
description: 
index_title: Address
hidden: 
keywords: 
tags: 
---

It is possible to extend the Identity verification integration by requesting an address check as part of a session.

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

If an address is extracted from both an ID document and supporting document, the supporting document address is used for the check. You may want to look at our document settings section to filter out specific documents in [auto$](/identity-verification/document-checking). 

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
<?php
  
$thirdPartyIdentityCheck = (new RequestedThirdPartyIdentityCheckBuilder())->build();

$sessionSpec = (new SessionSpecificationBuilder())
		// ..
		->withRequestedCheck($thirdPartyIdentityCheck)
		// ..
		->build();
{% /tab %}
{% tab language="python" %}
# COMING SOON
{% /tab %}
{% tab language="csharp" %}
var thirdPartyIdentityCheck = new RequestedThirdPartyIdentityCheckBuilder()
                                 .Build();

var sessionSpec = new SessionSpecificationBuilder()
    // ...
    .WithRequestedCheck(thirdPartyIdentityCheck)
    // ...
    .Build();
{% /tab %}
{% tab language="go" %}
var thirdPartyCheck *check.RequestedThirdPartyIdentityCheck
	thirdPartyCheck, err = check.NewRequestedThirdPartyIdentityCheckBuilder().
		Build()

	sessionSpec, err = create.NewSessionSpecificationBuilder().
//..
  WithRequestedCheck(thirdPartyCheck).
//..
{% /tab %}
{% tab language="json" %}
{
    "requested_checks": [
        {
            "type": "THIRD_PARTY_IDENTITY",
            "config": {
                "manual_check": "NEVER"
            }
        }
    ]
}
{% /tab %}
{% /code %}

To ensure the check can consistently be performed, we recommend creating a session that asks for one ID document, and one supporting proof of address document.