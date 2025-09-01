---
type: page
title: Liveness
listed: true
slug: portal-liveness
description: 
index_title: Liveness
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
We strongly suggest you read the sections above and understand the user flow and checks you want to enable.    </div>
   <div class="alert-links"> 
   </div>
</div>
{% /html %}

A requested check to assess whether the document scan is being performed by a real person, and not someone wearing a mask or an automated system.

You can choose the liveness type used in the flow. For more details on the different types, please see this [page](/identity-verification/liveness#liveness-types). We reccomend using 'Passive' liveness.

You can allocate how many retries you want the user to complete. We recommend a maximum of 3.

{% image url="https://uploads.developerhub.io/prod/kvAX/e3azzk684ptqp0kazrcm7zgwdyith23aqtj8366gwz80xwn57p8c0cugyj24s02y.png" caption="Application &gt; Portal preferences" mode="responsive" height="938" width="1076" %}
{% /image %}

For several American states (currently Texas, Illinois and Washington US states*), the law mandates that you must collect the user’s specific consent to collect their biometric details for our liveness or face matching feature to be compliant with the US legislation.

*and any other countries or states within countries
If you choose to only request specific consent in the above "territories" you must provide details of the effective geo location software you use to prevent any individuals located in one of these territories accessing the Yoti service without prior giving specific consent.