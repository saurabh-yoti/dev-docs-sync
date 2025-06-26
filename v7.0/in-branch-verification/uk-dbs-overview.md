---
type: page
title: Overview
listed: false
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

{% badge type="custom" text="SDKs" /%}  Coming soon!

The overview below details the entities and data flows.

{% badge type="warning" text="Help" /%} If you need any help please email [clientsupport@yoti.com](mailto:clientsupport@yoti.com).

{% html %}
<div class="alert-BYS">
   <div class="alert-title" id="BYS">
      Before you start
   </div>
   <div class="alert-text" >
      You will need the Yoti App on your phone and to have registered your business with Yoti. Click here for more info.
   </div>
   <div class="alert-links"> 
         <a target="_self" href="https://developers.yoti.com/visual-review-check/getting-started">View Onboarding with Yoti</a>
      <a target="_self" href="https://developers.yoti.com/visual-review-check/production-keys">View Generate API Keys</a> 
   </div>
</div>
{% /html %}

---

## Technical overview

### Feature list

The UK_DBS service provides three checks, please see below for features available for you to configure within your session.

{% table widths="310,0,204" %}
| Check Name | Description | Resources | In person check | 
| ---- | ---- | ---- | ---- | 
| PROFILE_DOCUMENT_MATCH | Visual check of the documents the applicant brought with them matches the submitted applicant profile. | 3x Document Resource | ✅ | 
| DOCUMENT_SCHEME_VALIDITY_CHECK | Checks the documents themselves fit within the standards of that scheme. E.g. validity of certain documents. | 3x Document Resource | ✅ | 
| IBV_VISUAL_REVIEW_CHECK | A visual review of the document. | 3x Document Resource | ✅ | 
{% /table %}

For a full extended list of all the checks and services available please check our or[ In branch verification documentation](/identity-verification/in-branch-overview) and our [Identity verification documentation. ](/identity-verification/overview#feature-list)

### Document list

Yoti only provides a capture service, we do not extract the data of these documents when using the UK_DBS feature.

Currently Yoti only supports UK documents for this service.

{% table %}
| Document | Backend name | Yoti Type | DBS group | 
| ---- | ---- | ---- | ---- | 
| Passport | PASSPORT | ID | 1 | 
| Driving license | DRIVING_LICENCE | ID | 1 | 
| National ID | NATIONAL_ID | ID | 1 | 
| British residence permit | RESIDENCE_PERMIT | ID |  | 
| Utility bill | UTILITY_BILL | Supplementary doc | 2b | 
| Bank statement | BANK_STATEMENT | Supplementary doc | 2b | 
| Council tax bill | COUNCIL_TAX_BILL | Supplementary doc | 2b | 
| Phone bill | PHONE_BILL | Supplementary doc |  | 
{% /table %}

Coming soon:

{% table %}
| Document | Backend Name | Yoti Type | DBS group | 
| ---- | ---- | ---- | ---- | 
| HM Forces ID Card | MILITARY_CARD | Supplementary doc | 2a | 
| PASS Card | PASS_CARD | Supplementary doc |  | 
| Firearms Licence | FIREARMS_LICENCE | Supplementary doc | 2a | 
| Birth Certificate (within 12 months of DOB) | BIRTH_CERTIFICATE_UNDER_12_MONTHS | Supplementary doc | 1 | 
| Birth Certificate (issued after 12 months from DOB) | BIRTH_CERTIFICATE | Supplementary doc | 2a | 
| Adoption Certificate | ADOPTION_CERTIFICATE | Supplementary doc | 2a | 
| Paper Driving Licence | DRIVING_LICENCE | Supplementary doc | 2a | 
| Marriage/Civil Partnership Certificate | MARRIAGE_CERTIFICATE | Supplementary doc | 2a | 
| Bank Opening Letter | ACCOUNT_OPENING_LETTER | Supplementary doc | 2b | 
| Benefit Statement | BENEFIT_STATEMENT | Supplementary doc | 2b | 
| Mortgage Statement | MORTGAGE_STATEMENT | Supplementary doc | 2b | 
| Financial Statement | FINANCIAL_STATEMENT | Supplementary doc | 2b | 
| P45 or P60 Statement | EMPLOYEE_TAX_FORM | Supplementary doc | 2b | 
| Employment Sponsorship Letter | EMPLOYMENT_SPONSORSHIP_LETTER | Supplementary doc | 2b | 
| Immigration Document/Visa/Work Permit | IMMIGRATION_DOCUMENT | Supplementary doc | 2a | 
| Education letter | EDUCATION_LETTER | Supplementary doc | 2b | 
| DVLA V5 or V5C/2 | DVLA_FORM | Supplementary doc | 1 | 
{% /table %}

---

## The user flow

{% image url="https://res.cloudinary.com/developerhub/image/upload/v1639660764/v2_2762/o0ev0dkutbqy1gormfee.jpg" mode="responsive" height="2513" width="1634" %}
{% /image %}