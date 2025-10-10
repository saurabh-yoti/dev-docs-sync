---
type: page
title: View sessions in portal
listed: true
slug: view-sessions-in-portal
description: 
index_title: View sessions in portal
hidden: 
keywords: 
tags: 
---

You have the option to view your sessions in a portal view if you have completed an API integration.

{% html %}
<div class="alert-BYS">
   <div class="alert-title" id="BYS">
      Before you start
   </div>
   <div class="alert-text" >
Get familiar with the portal and session results.   </div>
   <div class="alert-links"> 
         <a target="_self" href="https://developers.yoti.com/identity-verification/portal-session-results">Portal results</a>        
   </div>
</div>
{% /html %}

You may already have an API integration completed or you may want to enable this from the beginning. Please see below for which preference you are.

**Note - If the register key pair button does not appear as an option, it's likely the key has already been registered. Please do not attempt to generate a new key pair, as this could cause your existing integration to break. Go straight to the Portal Users tab and add a user.**

If you wish to enable this please follow the steps below:

1. Head to your [Hub](https://hub.yoti.com/iam/login) account. 
2. Find your service
3. Press REGISTER YOUR KEY PAIR

{% image url="https://uploads.developerhub.io/prod/kvAX/uic7bkfcp8tqomztkub5stpmmaycmsvzgfdofjlagmsene5wozlg6irvl7baspp6.png" caption="Hub &gt;&gt; Service &gt;&gt; Keys" mode="responsive" height="2132" width="2154" %}
{% /image %}

After this, you will have to add your current PEM file to the pop-up and give consent.

{% image url="https://uploads.developerhub.io/prod/kvAX/kwru6d3xgmq7a18gts9eutpoibgj1wx8gaqkj0egx0fh5mk15meva1s2hgy31p0v.png" caption="Hub &gt;&gt; Application &gt;&gt; Keys &gt;&gt; Register your key" mode="set" height="571.7734375" width="580" %}
{% /image %}

{% badge type="info" text="Hint" /%} You will not be able to review old sessions. 

If you haven't used the portal at all, you will need to continue with the following steps:

1. Adding a [Portal user](/identity-verification/add-users)
2. Logging on to the [Portal](/identity-verification/login)

---

## View your sessions

1. [auto$](/identity-verification/login) to the portal
2. You will now see that the home screen has enabled view API sessions.

{% image url="https://image-archive.developerhub.io/image/upload/v2_2762/wcrdgjtnlpocuu9ho00i/1639922790.png" caption="Login portal &gt; Select application" mode="responsive" height="356" width="376" %}
{% /image %}

3. The layout and results will follow the same as described in our portal[ session results section.](/identity-verification/portal-session-results)

**Note:** sessions created through the API will not appear on the "View sessions" link