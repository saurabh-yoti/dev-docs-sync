---
type: page
title: Add signers
listed: true
slug: add-signers
description: 
index_title: Add signers
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
You will need to have added a document to the portal.   </div>
   <div class="alert-links"> 
   </div>
</div>
{% /html %}

Here you can add the signer details. Add the following attributes:

- Name
- Email address - do not worry if you get this wrong. We will let you know and you can edit the details and re-send.
- Role

{% image url="https://uploads.developerhub.io/prod/kvAX/u6a0ixulamwe79luqraj0zs8cqgpi9xu3bnjhrmzh9h7y3bm1liwdrgrec9sducn.png" caption="Send a document &gt; Signers" mode="responsive" height="1360" width="1714" %}
{% /image %}

{% badge type="info" text="Hint" /%} You can add multiple people to sign the same document.

---

## Add Yoti authentication

A unique feature for our eSignatures platform is the ability to add a Yoti verification on top the signature.

To add the Yoti authentication:-

- Press the three dots, next to the "Role" input box.
- Click on "verify identity with digital id".
- Add which extra attributes you wish to have associated with the signature.

{% image url="https://uploads.developerhub.io/prod/kvAX/zt5vagu2l8zmqmn6vezrj83on73ulaz2tl8x2adj4seaoim56756g251a8soyz6r.png" caption="Send a document &gt; Signers &gt; Verify with Yoti." mode="responsive" height="1292" width="1642" %}
{% /image %}

{% badge type="info" text="Hint" /%} You can also add a one time code for extra security. Please see next section.

### Video explainer

{% html %}
<p style="padding:49.74% 0 0 0;position:relative;"><iframe src="https://player.vimeo.com/video/648540579?h=c96c996211&amp;badge=0&amp;autopause=0&amp;player_id=0&amp;app_id=58479&dnt=1" frameborder="0" allow="autoplay; fullscreen; picture-in-picture" allowfullscreen style="position:absolute;top:0;left:0;width:100%;height:100%;" title="(4) Adding Yoti Verification to a Document VIMEO.mp4"></iframe></div><script src="https://player.vimeo.com/api/player.js"></script>
{% /html %}

---

## Bulk upload

You can also upload a bulk send of signers. You will need a CSV ready! Yoti will provide you the template, click start bulk send.

{% html %}
<div class="alert-GTK">
    <div class="alert-title" id="GTK">
        Good to know
    </div>
    <div class="alert-text">
       The bulk upload feature is available upon request.
    </div>
    <div class="alert-links"> 
        <a href="https://support.yoti.com/yotisupport/s/contactsupport">Contact us</a>
   </div>
</div>
{% /html %}

- Press: Start bulk send

{% image url="https://uploads.developerhub.io/prod/kvAX/1j7vztd4d04f63yu0o0lypvugenpgod4kk22v7riivfxu0ttu3yea0wpo149ot6i.png" mode="responsive" height="1150" width="1636" %}
{% /image %}

- You will have the option to upload a CSV / Download the template to then add users.

{% image url="https://res.cloudinary.com/developerhub/image/upload/v1628071246/v2_2762/cydeysjtfiz6so9wtlvf.png" caption="Bulk / Download" mode="responsive" height="257" width="745" %}
{% /image %}

- Once this upload is complete you will have the option to check errors and edit.

{% image url="https://res.cloudinary.com/developerhub/image/upload/v1628071423/v2_2762/s022kipoyaag2wyinzf8.png" caption="Confirm bulk upload" mode="responsive" height="444" width="958" %}
{% /image %}

{% html %}
<div class="alert-GTK">
    <div class="alert-title" id="GTK">
        Good to know
    </div>
    <div class="alert-text">
If any mistakes are made or you want to send a reminder there are options to do this after the envelope is sent.

    </div>
    <div class="alert-links"> 
       <a href="https://developers.yoti.com/eSignatures/view-documents#bounced-documents">Edit details</a>
      <a href="https://developers.yoti.com/eSignatures/view-documents#reminders">Reminders<a> 
    </div>
</div>
{% /html %}

---

## Add a non signer recipient

You can add a non signing recipient, who will receive a copy of the completion pack. 

The non signing recipient (CC recipient) does not receive an invitation to the envelope, once the envelope is complete and all signers have signed then the completion pack email is triggered and is sent to all recipients including non signing recipients.

{% image url="https://uploads.developerhub.io/prod/kvAX/upz1l707yeafgzpsie35rmvw91duhrmkvrsle3puu905der4qjbqst2m4slbq9m0.png" caption="Non signer flow" mode="responsive" height="1156" width="1652" %}
{% /image %}

To enable a non signer recipient click: Receives a copy.