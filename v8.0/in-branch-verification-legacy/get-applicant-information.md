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

There are five steps to follow to integrate the UK DBS service.

1. Get applicant information
2. Generate signed request
3. Create the session
4. Send instructions
5. Generate results

The first step is not available via the API. 

---

## Get applicant information

In order to create a session you must first collect information about the customer including: 

1. Name of the applicant - {% badge type="info" text="Hint" /%} This should be the applicants full legal name and MUST match what is on the ID document. Make this very clear to your users. 
2. Address of the applicant - See applicant profile for structured address format. 
3. Date of birth of the applicant - This must be in yyyy-mm-dd format.

This information will be used to fill out the applicant profile, which is then cross referenced against the information on the customers documents when they are brought in for the checks.

---

## Get Documents

In addition to the applicant information, you will also need the applicant to select the documents that they want to bring to be checked. 

A list of documents that we support can be found [here](https://developers.yoti.com/in-branch-verification/uk-dbs-overview). 

{% badge type="info" text="Hint" /%} The customer will need to make sure they have the documents that they select, and that they are within the correct date. If one document is incorrect they will have to restart the process.

---

## Branch look up

In order for the customer to know which branch to visit please use the Post Office branch look up API.

For further information around accessing this API, please contact support at clientsupport@yoti.com.