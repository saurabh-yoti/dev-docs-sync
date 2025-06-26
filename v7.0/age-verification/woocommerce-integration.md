---
type: page
title: Integration guide
listed: true
slug: woocommerce-integration
description: 
index_title: Integration guide
hidden: 
keywords: 
tags: 
---

{% html %}
<div class="alert-GTK">
    <div class="alert-title" id="GTK">
        Good to know
    </div>
    <div class="alert-text">
This integration is in BETA. Please help us improve by providing feedback. 
    </div>
 <div class="alert-links"> 
      <a href="mailto:clientsupport@yoti.com"> Contact us </a> 
   </div>

   </div>
</div>
{% /html %}

Welcome to the developer documentation for integrating with Age verification with WooCommerce. 

The integrations steps are as follows:

1. Download the plugin
2. Install the plugin
3. Add your API Key and Bearer token
4. Activate the plugin for the relevant products

---

## Download the plugin

Download the plugin from [here](https://www.yoti.com/wp-content/uploads/woocommerce-yoti-plugin-1.0.zip). 

---

## Install the plugin

Head to your WooCommerce set up. 

- Click on Plugins
- Click ‘Add New’

{% image url="https://res.cloudinary.com/developerhub/image/upload/v1638282525/v2_2762/v4l4dubosotugzyhf6vt.png" caption="Settings &gt; Plugins &gt; Add new" mode="responsive" height="1368" width="2878" %}
{% /image %}

- Click ‘Upload Plugin’
- Click ‘Choose file’
- Choose the zip file and click ‘install now’.

{% image url="https://uploads.developerhub.io/prod/kvAX/f6hskk27d0p1y7u0wy6kgjuf2lgxgh89f6dqn1lm655c5fxoldssr9d0wyqznn8n.png" caption="Settings &gt; Plugins &gt; Add new &gt;Upload &gt; Activate" mode="responsive" height="821" width="2536" %}
{% /image %}

- Click ‘Activate now’

---

## Add API Key

{% html %}
<div class="alert-BYS">
   <div class="alert-title" id="BYS">
      Before you start
   </div>
   <div class="alert-text" >
      You will need to have completed Onboarding and generated API keys. 
   </div>
   <div class="alert-links"> 
      <a href="https://developers.yoti.com/age-verification/getting-started"> Onboarding </a>
   </div>
</div>
{% /html %}

- Head to the settings page

{% image url="https://res.cloudinary.com/developerhub/image/upload/v1638377952/v2_2762/jdmd3v8jax8hwjvlw6s8.png" mode="responsive" height="200" width="1520" %}
{% /image %}

- Add the sdkID and Bearer token
- Select which checks you want to enable

{% image url="https://uploads.developerhub.io/prod/kvAX/o1kwv7y3rx9cfash5sz5r729raedbq84rw92ub2xfmc0atcsjofha1tnprn2jgne.png" caption="Settings &gt; Yoti Age Verification" mode="responsive" height="1596" width="1518" %}
{% /image %}

Congratulations - the setup is complete.

---

## Using the plugin

Now that the plugin is installed head to your products.

{% image url="https://res.cloudinary.com/developerhub/image/upload/v1638282764/v2_2762/vgqfczqwivj7wtfshsrw.png" caption="All products" mode="responsive" height="1046" width="2204" %}
{% /image %}

- Now select the products you wish to age verify for.
- Finally choose which age to verify for.
- Click ‘Apply’ and you’re done!

---

## User flow

You will need to decide how you want your user flow to be. Please see below as an example:

1. The user will choose which product they want to purchase.

{% image url="https://uploads.developerhub.io/prod/kvAX/rk9h6q70b76loag11881t7zoy45pcjqrqfmym4ratlpa7ac1p34ce54r7uwxaj92.png" caption="User shop" mode="responsive" height="421" width="1028" %}
{% /image %}

2. The user will proceed to check out.

{% image url="https://uploads.developerhub.io/prod/kvAX/rb1v62hrqy93tgl049s6k1cxpq2edxdh7n82g4qex8wer1c860d9h93j820js12k.png" caption="Checkout" mode="responsive" height="770" width="1383" %}
{% /image %}

3. The user will fill in their personal details.

{% image url="https://uploads.developerhub.io/prod/kvAX/j59v3ce9v4mjcm40bgcnvplrojrhle3hinxkaunzr86axwwyskmkguzt79ap8i8d.png" caption="Personal details" mode="responsive" height="614" width="1028" %}
{% /image %}

4. The user will be prompted to complete Yoti Age verification. 

{% image url="https://uploads.developerhub.io/prod/kvAX/d0xn7pne6hwpyctjy2aoylioksgrvlwqmsj01tcd9hj3xqbeh58afw2te7xiodqs.png" caption="Yoti Age Verification" mode="responsive" height="713" width="1507" %}
{% /image %}

5. The user will perform an age request and will receive a confirmation message.

{% image url="https://uploads.developerhub.io/prod/kvAX/i746noj5q8t2lvygt3mo5vt0qk41hbusmb6t8leg5w3uf91o1426ggxwgs4untab.png" caption="Yoti Age Verification confirmation screen" mode="responsive" height="655" width="1383" %}
{% /image %}

---

## Review results

Head to your WooCommerce admin page. 

- Go to Orders
- See status of Age Verified 

{% image url="https://uploads.developerhub.io/prod/kvAX/l4g7wz8hk22obsq7gl62y5d4wjmznrmygddlcdm2k4tnc6a3ou0eeinyqcje0l5y.png" caption="Results page" mode="responsive" height="643" width="1507" %}
{% /image %}