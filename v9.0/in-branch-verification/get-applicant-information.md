---
type: page
title: Get applicant information
listed: true
slug: get-applicant-information
description: 
index_title: Get applicant information
hidden: 
keywords: 
tags: 
---

## [Get applicant information](https://developers.yoti.com/in-branch-verification/get-applicant-information#get-applicant-information)

In order to create a session you must first collect information about the customer including:

1. Name of the applicant - {% badge type="info" text="Hint" /%} This should be the applicants full legal name and MUST match what is on the ID document. Make this very clear to your applicants. If there has been any change of name or variations of name between documents, these will be rejected. All middle names must be included.
2. Address of the applicant - See applicant profile for structured address format.
3. Date of birth of the applicant - This must be in yyyy-mm-dd format.

This information will be used to fill out the applicant profile, which is then cross referenced against the information on the customers documents when they are brought in for the checks.

---

## [ Select Documents](https://developers.yoti.com/in-branch-verification/get-applicant-information#get-documents)

In addition to the applicant information, you will also need the applicant to select the documents that they want to bring to be checked. You will need to specify the exact document type as well as the country code.

A list of documents that we support can be found [here](/in-branch-verification/overview).

{% badge type="info" text="Hint" /%} The customer will need to make sure they have the documents that they select, and that they are within the correct date. If one document is incorrect they will have to restart the process.

---

## [Branch look up](https://developers.yoti.com/in-branch-verification/get-applicant-information#branch-look-up)

**The In-Branch Verification service is not available in every Post Office, so it's critical that customers are directed to an enabled location. Post Office has made it's Location & Data Services API available for organisations to use, so that a customer can select from their nearest enabled branch and have this address included on the issued customer letter. The session is not locked to this branch only, so a user may use the Post Office Branch Finder ([https://www.postoffice.co.uk/branch-finder](https://www.postoffice.co.uk/branch-finder)) and select the 'Identity Services &gt; In Branch Verification' option to find other branches should they want to go to another branch after session creation.**

**In order for the customer to know which branch to visit please use the Post Office location and data services API, details can be found here ([auto$](/in-branch-verification/post-office-lookup)).**