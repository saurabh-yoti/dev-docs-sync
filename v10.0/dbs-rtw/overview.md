---
type: page
title: Overview
listed: true
slug: overview
description: 
index_title: Overview
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
       Yoti and Post Office EasyID are a certified IDSP, further information regarding our certification can be found <a href="https://www.yoti.com/blog/yoti-uk-government-approved-dbs-right-to-work-rent-checks/">here</a>.
    </div>
    <div class="alert-text">
       We do appreciate any feedback on this service. You may leave feedback through our feedback form, or alternatively get in touch through the contact email listed below.
    </div>
    <div class="alert-links"> 
        <a href="https://forms.gle/vKqNLnt66rE3JwBE6">Feedback form</a>
        <a target="_self" href="https://support.yoti.com/yotisupport/s/contactsupport">Contact us</a>
   </div>
</div>
{% /html %}

This documentation serves as an integration guide for Yoti & Post Office’s new services:

1. Digital identity for DBS
2. Right to Work
3. Right to Rent 

This document is intended primarily for a technical audience, but there are also notes that may be useful for product designers and product managers.

The products that will be extended with these services are:

- [Identity Verification](https://developers.yoti.com/identity-verification/overview) (IDV)
- [Digital ID](https://developers.yoti.com/digital-id/overview) (App)
- [In-Branch Verification](https://developers.yoti.com/in-branch-verification) (IBV)

There are two sets of rules around how identity must be checked as part of a DBS check or when proving RTW/R under consideration.

1. **Existing in-person verification:** Historically, DBS identity
checks have required physical sighting of a document, either by the employer themselves or a responsible agent involved in the process, including by the Post Office In-Branch Verification service. 
2. **New digital verification:** Also applicable to “Right to Work” checks for UK and Irish citizens. Once an IDSP is certified, the DBS will allow, for the first time, use of digital ID as accepted proof of ID before a DBS check is undertaken. The rules for this digital route for DBS do not specify individual documents that can be used (as is the case in the existing document-based route), rather they align with GPG45 levels of assurance under the DCMS Identity and Attributes Trust Framework (IATF). There are however constraints on the documents that can be used for a digital right to work and rent check; namely UK or Irish Passports.                             

Yoti has developed a new request and response format to cater specifically for the new requirements of the digital route, for both the DBS scheme and the Home Office Right to Work/Rent scheme. 

The supported schemes are:

{% table widths="" %}
| Check | Type | GPG45 Level | 
| ---- | ---- | ---- | 
| DBS | DBS Basic | Medium | 
| DBS | DBS Standard / Enhanced | High | 
| RTW & RTR |  | Medium | 
| DBS + RTW combo | DBS Basic | Medium | 
| DBS + RTW combo | DBS Standard / Enhanced | High | 
{% /table %}

Please note that the DBS scheme rules for Standard / Enhanced disclosures require GPG45 High, and are therefore encouraging clients to utilise the Digital ID app routes where they require GPG45 High. This is because the Digital ID app, both Yoti and Easy ID, have more routes available to reach this desired level of assurance, due to having the ability to scan and verify Passports through an NFC chip read.

### Digital ID and IDV integrations

This documentation focuses on the request and response content, other integration details remain as per our existing integration documentation for [Digital ID](https://developers.yoti.com/digital-id/overview) and [Embedded IDV](https://developers.yoti.com/identity-verification/overview). 

We have deliberately taken care to align the request and response formats across the two products, while allowing for differences between the product sets. For example, it is possible to request a ‘scheme compliant share’ from a reusable digital ID app user, and at the same time request other information from that user’s digital ID not required by the scheme itself (e.g. verified email address, verified phone number, etc.)

### IBV integration

Our [In-Branch Verification (IBV)](https://developers.yoti.com/in-branch-verification) product caters for the existing ‘document-based’ identity verification rules set by the DBS.

This route requires

- The relying party to send our API the personal details (name, current address and date of birth) of the person being verified when the session is created.
- The relying party to determine which documents the person being verified will bring to the Post Office branch, to be specified in the session creation request.
- Which branch they will go to (the Post Office ‘branch finder’ API may be used for this)
- For compliance with the DBS policy, the customers' documents are checked by the Post Office postmaster, with no additional processing completed by the back office or security centre. Additional document validation and identity verification services are available as supported by the Yoti technology and the security centre , however these are not required. The Postmaster performs a full in-person comparison of the details provided by the relying party at ‘session creation time’ to the evidence presented by the applicant, including checking that their documents meet the DBS validity rules.
- Our expectation is for the DBS to mature their in person verification policies and in future we intend to offer a Digital ID based (GPG45-aligned) service through the Post Office branch.

In the following sections we detail the request and response structures that facilitate identity verification to the DCMS IATF, DBS and RTW/R schemes. We will first cover ‘reusable digital ID’ and then ‘embedded IDV’, and IBV. Details of the ‘identity profile’, which is common to digital ID and IDV integrations and forms the main substance of the response is also shared.

---

## Useful resources

{% table widths="" %}
| Description | Link | 
| ---- | ---- | 
| Yoti Website Blog | [https://www.yoti.com/business/right-to-work/](https://www.yoti.com/business/right-to-work/) | 
| Good Practice guide | [https://www.yoti.com/blog/good-practice-guide-45-gpg-45/](https://www.yoti.com/blog/good-practice-guide-45-gpg-45/) | 
| DBS digital identity verification guidance | [https://www.gov.uk/government/publications/dbs-identity-checking-guidelines/dbs-digital-identity-verification-guidance](https://www.gov.uk/government/publications/dbs-identity-checking-guidelines/dbs-digital-identity-verification-guidance) | 
| Employers guide to right to work checks | [https://www.gov.uk/government/publications/right-to-work-checks-employers-guide/an-employers-guide-to-right-to-work-checks-17-january-2022-accessible-version](https://www.gov.uk/government/publications/right-to-work-checks-employers-guide/an-employers-guide-to-right-to-work-checks-17-january-2022-accessible-version) | 
| Identity profiles | [https://www.gov.uk/government/publications/identity-proofing-and-verification-of-an-individual/identity-profiles#medium-confidence](https://www.gov.uk/government/publications/identity-proofing-and-verification-of-an-individual/identity-profiles#medium-confidence) | 
{% /table %}