---
type: page
title: Glossary
listed: true
slug: glossary
description: 
index_title: Glossary
hidden: 
keywords: 
tags: 
---

See below for Yoti terminology:

{% table %}
| Yoti | Description | 
| ---- | ---- | 
| Sender | A sender is any user on that intends on sending documents. | 
| Signer | An email recipient of a sign request, sent by a sender or External API user. | 
| Envelope | A combination of the details set up by the sender including files, tags, signee information, reminders. | 
| Document | The files that are within a document. | 
| Coversheet file | A document generated once the document completed - each signer once they have signed the document | 
| XML file | A document generated once the document completed  that is legal proof of signing. | 
| Single envelope | A single envelope that can one or more signees and documents. | 
| Bulk envelope | More than one envelopes that have individual signees per envelope. | 
| Tags | Information or signatures requested by the sender to be filled by the signer. | 
| Reminders | Email notifications that can be set by a sender, and are sent to signers that have not yet signed to remind them to sign. | 
| Draft state | A envelope that has not yet been sent yet. Drafts are created on the Sender flow only when a user exits without saving. | 
| Template state | Senders often send out a similar documents and do not want to re-create and set up the document every time. A template is a document that contains the standard details and that can be copied and adapted before sending. | 
| Active state | Any document that is not archived despite signer states. | 
| Archive state | The envelope will be **withdrawn** so that it can no longer be signed or completed. All signers are notified via email and this action can not be undone. | 
| Role | A category of signer e.g. landlord or tenant | 
| Auth level | Authentication of the signer. | 
| Email Auth | An authentication level for the signer. This is authenticated through access to the email the document was sent. | 
| Yoti Auth | Strong authentication for the signer using Yoti verified email. The signer would have to scan a QR code to share the email attribute that has been verified with Yoti. Email can only be added to one Yoti account and uses 2fa. | 
| Signature | A digital signature requested by the sender and added to the document at by an authenticated signer through a click/interaction. | 
| Text field | A text field requested by the sender and able to be filled by an authenticated signer. | 
| Check box | A check box which can be optional (Boolean) or mandatory e.g. accepting terms which is requested by the sender. | 
| Yoti Attributes | Identity details of a signer that have been verified by Yoti e.g. name or date of birth. | 
{% /table %}