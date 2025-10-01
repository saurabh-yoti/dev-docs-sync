---
type: page
title: Overview
listed: true
slug: ibv-overview
description: 
index_title: Overview
hidden: 
keywords: 
tags: 
---

{% html %}
<div class="alert-BYS">
   <div class="alert-title" id="BYS">
      Before you start
   </div>
   <div class="alert-text" >
      You will need the Yoti App on your phone and to have registered your business with Yoti. Click here for more info.
   </div>
   <div class="alert-links"> 
         <a target="_self" href="https://developers.yoti.com/in-branch-verification/getting-started">View Onboarding with Yoti</a>
      <a target="_self" href="https://developers.yoti.com/in-branch-verification/production-keys">View Generate API Keys</a> 
   </div>
</div>
{% /html %}

In-Branch Verification is a service for organisations who require In-person  identity verification and document validation. This service will use Yoti's Identity verification capability combined with a face-to-face transaction to provide identity and proof of address document validation and identity verification to clients who require additional assurance to meet business risk or regulatory obligations, or to customers who require the additional assistance that a branch can provide.

There are three stages to an In-Branch Verification journey:

1. Customer selects documents online
2. Guidance and preparation
3. In branch flow 

### Customer selects documents online

In this step, you define what document types are required or accepted from your customer as well as which validation and verification services you would like to use as part of the identity verification. These include:

- Digitised documents with customer face capture
- Document validation
- Biometric facial matching of the customers image to photo ID
- Text extraction
- Third  party identity and address verification.

### Guidance and preparation

The aim is to facilitate the in branch service by ensuring the user has what they need before arrival.

They will:

- Give their contact information, pick a location and decide what documents to bring.
- The user will receive a PDF of instructions / a summary of the choices they made with where to go and what to bring.

### In branch flow

The aim is to go into the branch with your documents and instructions:

- Pass the documents to the branch, complete IDV check. 
- Take a photo of the user. 
- Receive a confirmation receipt. 

---

## Technical overview

{% image url="https://image-archive.developerhub.io/image/upload/v2_2762/mqct1abhftldekbzwput/1629398528.png" caption="Placeholder" mode="responsive" height="1304" width="1026" %}
{% /image %}

### At Home flow

1. The user will request an IBV session from your site. The user will be guided through the IBV flow.
2. First they will see an education screen highlighting the process. The user will then select and agree what documents they will provide to the branch.
3. The customer finds their nearest identity services branch in the online service. Yoti will provide a lookup service.
4. The user is then asked to enter their 
    1. Name
    2. Email address 
    3. Terms & Conditions to be accepted. 

5. The user can either download their PDF of instructions or an email with an attached PDF will be sent to the client of instructions and a transaction QR code is sent to the customer to bring to branch.

{% table widths="212" %}
| Name | Description | 
| ---- | ---- | 
| Document selection | Ability for user to pre select what documents they wish to share. \n\n\n\n- 1 UK ID document\n- 1 ID document \n- 1 Non photo document. | 
| Postcode lookup | The customer can enter their postcode to find the nearest branch to them. | 
| Contact details | The customer inputs their name, and email address twice. This is used to send a confirmation email and a PDF. | 
| Downloadable PDF | The customer will need to bring this to store with them. The page will contain:\n\n\n\n- A QR code used to continue the session in branch.\n- A reminder on the documents to bring\n- Payment details \n- Expiry date to complete the verification | 
{% /table %}

### In Branch flow

1. The customer will then head to the branch, the branch will facilitate the IBV transaction using the QR code to retrieve the document checking  requirements.  
2. The branch must ensure the customers documents are present. Yoti will provide guidance around this. 
3. The branch will take a photo of the user on the android device.
4. The branch will processes the documents for back-office checking and identity verification.
5. Once processing is completed, the branch will request a ‘session report’ from Yoti, detailing the outcomes of the IBV service.

{% html %}
<div class="alert-GTK">
    <div class="alert-title" id="GTK">
        Good to know
    </div>
    <div class="alert-text">
It's worth reading our Identity Verification documentation to understand how we complete the Yoti document review process    </div>
    <div class="alert-links"> 
       <a href="https://developers.yoti.com/identity-verification/overview">Identity verification</a>
    </div>
</div>
{% /html %}

## Feature list

The IBV service provides configurable checks, please see below for features available for you to configure within your session.

{% table widths="0,0,242,111" %}
| Name | Description | Resources | Type | Manual check available | 
| ---- | ---- | ---- | ---- | ---- | 
| Pre scanning check list | Ensure the customer has all the documents required present with them. | N/A | N/A | N/A | 
| Document authenticity | A request to assess the characteristics of a document, to determine the validity of the ID document. Yoti will perform multiple checks on a ID document.\n\nNFC can be enabled here. | 1x Document Resource | Asynchronous | ✅ | 
| Text extraction | A request to obtain the data printed visually on a document, in structured form. | 1x Document Resource | Asynchronous | ✅ | 
| Supporting documents | Yoti offers the ability to request additional documents to enhance the verification of the user. | 1x Document Resource | Asynchronous | ✅ | 
| Document comparison | If you request your users to upload more than one document we offer the ability to cross check the data | 2x Document Resource | Asynchronous | ❌ | 
| Address check | This check will facilitate an extra verification of a user by searching a person’s details against a collated database from various sources worldwide | 1x Document resource from:\n\n\n\n- document authenticity or supporting documents \n- text extraction. | Asynchronous | ✅ | 
| AML check | Extend the Identity verification integration by requesting an watchlist, PEPs and sanctions check as part of a session. | 1x Document resource from: \n\n\n\n- text extraction. | Asynchronous | ❌ | 
| Face match check | A request to assess whether the user's face matches the face on the ID document. | 1x Doc Resource & 1x Facematch Resource | Asynchronous | ✅ | 
{% /table %}