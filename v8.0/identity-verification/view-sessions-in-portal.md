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

You may already have an API integration completed or you may want to enable this from the beginning, please see below for which preference you are.

**Note - If register key pair does not appear as an option, it's likely the key has already been registered. Please do not attempt to generate a new key pair or this could cause your existing integration to break. Go straight to the Portal Users tab and add a user.**

If you wish to enable this please follow the steps below:

1. Head to your hub account. 
2. Find your application
3. Press REGISTER YOUR KEY PAIR

{% image url="https://res.cloudinary.com/developerhub/image/upload/v1639920110/v2_2762/oihchihv8hg0vzlwozjx.png" caption="Hub &gt; Application &gt; Keys" mode="responsive" height="807" width="912" %}
{% /image %}

After this you will have to add your current PEM file to the pop up and give consent.

{% image url="https://res.cloudinary.com/developerhub/image/upload/v1639920165/v2_2762/afhrf3sl2zfheotmen2l.png" caption="Hub &gt; Application &gt; Keys &gt; Register your key" mode="600" height="1000" width="1048" %}
{% /image %}

{% badge type="info" text="Hint" /%} You will not be able to review old sessions. 

If you havent used the portal at all you will need to continue with the following steps:

1. Adding a [collaborator](/identity-verification/portal-guide#add-users)
2. Logging on to the [portal.](https://developers.yoti.com/identity-verification/login)

---

## View your sessions

1. [Log in](/identity-verification/login) to the portal
2. You will now see the home screen has enabled view API sessions.

{% image url="https://res.cloudinary.com/developerhub/image/upload/v1639922790/v2_2762/wcrdgjtnlpocuu9ho00i.png" caption="Login portal &gt; Select application" mode="responsive" height="356" width="376" %}
{% /image %}

3. The layout and results will follow the same as described in our portal[ session results section.](/identity-verification/portal-session-results)