---
type: page
title: Overview
listed: true
slug: uk-dbs-overview
description: 
index_title: Overview
hidden: 
keywords: 
tags: 
---

Welcome to the developer documentation for integrating the UK_DBS integration.

You can integrate this service in one way currently:

{% badge type="custom" text="API" /%} Yoti gives you the option to use our API directly.

{% badge type="custom" text="SDKs" /%} Use our SDK to handle request authentication.

The overview below details the entities and data flows.

{% badge type="warning" text="Help" /%} If you need any help please email [clientsupport@yoti.com](mailto:clientsupport@yoti.com).

{% html %}
<div class="alert-BYS">
   <div class="alert-title" id="BYS">
      Before you start
   </div>
   <div class="alert-text" >
			You will need to access your Yoti Hub account with an e-mail & password or using the Yoti mobile app and to have registered your business with Yoti. Click below for more info.
   </div>
   <div class="alert-links"> 
         <a target="_self" href="https://developers.yoti.com/visual-review-check/getting-started">View Onboarding with Yoti</a>
      <a target="_self" href="https://developers.yoti.com/visual-review-check/production-keys">View Generate API Keys</a> 
   </div>
</div>
{% /html %}

{% callout type="info" title="This document concerns the Disclosure & Barring Service Digital ID integration" %}
This follows the UK scheme that applies to England, Wales and Northern Ireland

This is different to the scheme followed by Disclosure Scotland
{% /callout %}

---

## Technical overview

### Feature list

The UK_DBS service provides three checks, please see below for features available for you to configure within your session.

{% badge type="custom" text="Note" /%} Our DBS service is based around UK regulations that apply in England, Wales and Northern Ireland, but not Scotland.

{% table widths="310,0,204" %}
| Check Name | Description | Resources | In person check | 
| ---- | ---- | ---- | ---- | 
| PROFILE_DOCUMENT_MATCH | Visual check of the documents the applicant brought with them matches the submitted applicant profile. | 3x Document Resource | ✅ | 
| DOCUMENT_SCHEME_VALIDITY_CHECK | Checks the documents themselves fit within the standards of that scheme. E.g. validity of certain documents. | 3x Document Resource | ✅ | 
| IBV_VISUAL_REVIEW_CHECK | A visual review of the document. | 3x Document Resource | ✅ | 
{% /table %}

For a full extended list of all the checks and services available please check our or[ In branch verification documentation](/identity-verification/in-branch-overview) and our [Identity verification documentation. ](/identity-verification/overview#feature-list)

### Document list

{% table %}
| Document | Backend name | Yoti Type | 
| ---- | ---- | ---- | 
| Passport | PASSPORT | ID | 
| Driving license | DRIVING_LICENCE | ID | 
| National ID | NATIONAL_ID | ID | 
| Biometric residence permit | RESIDENCE_PERMIT | ID | 
| Utility bill | UTILITY_BILL | Supplementary doc | 
| Bank statement | BANK_STATEMENT | Supplementary doc | 
| Council tax bill | COUNCIL_TAX_BILL | Supplementary doc | 
| Phone bill | PHONE_BILL | Supplementary doc | 
| HM Forces ID Card | MILITARY_CARD | Supplementary doc | 
| PASS Card | SUPPLEMENTARY_PASS_CARD | Supplementary doc | 
| Firearms Licence | FIREARMS_LICENCE | Supplementary doc | 
| Birth Certificate (within 12 months of DOB) | BIRTH_CERTIFICATE_ISSUED_WITHIN_12_MONTHS_OF_BIRTH | Supplementary doc | 
| Birth Certificate (issued after 12 months from DOB) | BIRTH_CERTIFICATE | Supplementary doc | 
| Adoption Certificate | ADOPTION_CERTIFICATE | Supplementary doc | 
| Paper Driving Licence | PAPER_DRIVING_LICENCE | Supplementary doc | 
| Marriage/Civil Partnership Certificate | MARRIAGE_CERTIFICATE | Supplementary doc | 
| Bank Opening Letter | ACCOUNT_OPENING_LETTER | Supplementary doc | 
| Benefit Statement | BENEFIT_STATEMENT | Supplementary doc | 
| Mortgage Statement | MORTGAGE_STATEMENT | Supplementary doc | 
| Financial Statement | FINANCIAL_STATEMENT | Supplementary doc | 
| P45 or P60 Statement | EMPLOYEE_TAX_FORM | Supplementary doc | 
| Employment Sponsorship Letter | EMPLOYMENT_SPONSORSHIP_LETTER | Supplementary doc | 
| Immigration Document/Visa/Work Permit | IMMIGRATION_DOCUMENT | Supplementary doc | 
| Education letter | EDUCATION_LETTER | Supplementary doc | 
| DVLA V5 or V5C/2 | DVLA_FORM | Supplementary doc | 
{% /table %}

---

## The user flow

{% image url="https://res.cloudinary.com/developerhub/image/upload/v1639660764/v2_2762/o0ev0dkutbqy1gormfee.jpg" mode="responsive" height="2513" width="1634" %}
{% /image %}