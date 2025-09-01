---
type: page
title: WooCoommerce Integration guide
listed: true
slug: woocommerce-integration
description: 
index_title: WooCommerce
hidden: 
keywords: 
tags: 
---

{% callout type="info" title="Good to know" %}
This integration is in BETA. Please help us improve by providing feedback.

[Contact us](https://support.yoti.com)
{% /callout %}

Welcome to the documentation for integrating Yoti Age verification (AV) with WooCommerce.

Following are the integration steps:

1. Download the plugin
2. Install the plugin
3. Add your keys and configure the plugin options
4. Enable Age verification for relevant products

---

## Download the plugin

Download the plugin installation file from [this link](https://www.yoti.com/wp-content/uploads/2024/03/yoti-age-verification-woocommerce_v_03_24.zip).

---

## Install the plugin

Head to your WooCommerce set-up. 

- Open Plugins page from the left menu
- Then, click the ‘**Add New Plugin**’ button

{% image url="https://uploads.developerhub.io/prod/kvAX/px22aefxqfvf68p0y9om3g19ffk4k0cgg2toqlt32ieou7cuijugmv3f25vrxm08.jpeg" caption="Settings &gt; Plugins &gt; Add New Plugin" mode="responsive" height="792" width="1920" %}
{% /image %}

- After, click the ‘**Upload Plugin’** button
- Click the ‘**Choose file**’ button and select the plugin zip file
- Then click the ‘**Install Now**’ button

{% image url="https://uploads.developerhub.io/prod/kvAX/c3pdim3tot3qd220uwbz23qq8dooabjxjbysfbsuovjy20sx1ivl6kj0gnscgqdm.jpeg" caption="Settings &gt; Plugins &gt; Add New Plugin &gt; Upload Plugin  &gt; Install Now" mode="responsive" height="785" width="1920" %}
{% /image %}

- Finally, click on ‘**Activate**’ link below the installed plugin name

{% image url="https://uploads.developerhub.io/prod/kvAX/dhg184z46rgkb5bg0sb7t1bbglf0y43msmvypp7rl1emmk6kgk1ob0iq4focsyc1.jpeg" caption="Settings &gt; Plugins &gt; Activate" mode="responsive" height="409" width="1920" %}
{% /image %}

---

## Add keys and configure the plugin

{% callout type="warning" title="Before you start" %}
You will need to have completed Onboarding and generated API keys.

[Onboarding](https://developers.yoti.com/age-verification/getting-started)
{% /callout %}

- Open the plugin settings page by going to '**Settings -&gt; Yoti Age Verification WooCommerce**' from the left menu
- Add the SDK ID and API Key 
- Set the default age threshold and enable verification methods
- Configure the AV trigger point, auto-redirection and webhook options

{% image url="https://uploads.developerhub.io/prod/kvAX/5t9z4w78ybsrihu50wv76iv5k86elqq5xp1532lkboebybkyjpkulsz9rip3ta1w.jpeg" caption="Settings &gt; Yoti Age Verification WooCommerce" mode="responsive" height="1090" width="1920" %}
{% /image %}

- Set the AV retention period for logged-in and non logged-in users
- Then, click the '**Save Changes**' button

{% image url="https://uploads.developerhub.io/prod/kvAX/usj4zmhwv577uje2z3eopbep6bp48n58mjdqxgcnyqfnh6hvtmvai1g7spmij6p9.jpeg" caption="Settings &gt; Yoti Age Verification WooCommerce" mode="responsive" height="460" width="1920" %}
{% /image %}

Congratulations - the setup is complete.

---

## Enable age verification for products

Now that the plugin is installed head to your products by going to '**Products -&gt; All Products**'.

- For each relevant product, set the Age threshold and enable/disable Age verification. Make sure to click the individual '**Save**' buttons after changing the product configuration.

{% image url="https://uploads.developerhub.io/prod/kvAX/sxvm9gvr0vfkq8ma7wdxfltui3x8cngc56pqi46g6gw3wzlpb0ycw03e3t1qsicq.jpeg" caption="Products -&gt; All Products" mode="responsive" height="627" width="1920" %}
{% /image %}

- It's also possible to use '**Bulk actions**' dropdown to set Age threshold and enable/disable Age verification for multiple products simultaneously. Click '**Apply**' after selecting the products and desired action.

{% image url="https://uploads.developerhub.io/prod/kvAX/qbs02estbnjsetkmwj28vvzasi7bubhfbrjgh7h5l4tetjixo1t56yqjqu6n2yvq.jpeg" caption="Products -&gt; All Products" mode="responsive" height="639" width="1920" %}
{% /image %}

---

## End-user flow

You will need to decide how you want your user flow to be. Please see below as an example:

1. The user will choose which product they want to purchase.

{% image url="https://uploads.developerhub.io/prod/kvAX/nsxgz5fpu3q4iwfsyuchwdpepotos8kgs3ipg67sokouv0je5v63ec8y9ssvca2d.jpeg" caption="User shop" mode="responsive" height="952" width="1920" %}
{% /image %}

2. The user will then go to the cart page. The products requiring age verification will show '**Age-restricted product**' next to them.

{% image url="https://uploads.developerhub.io/prod/kvAX/dmj5v2o0qugwq2k4swn42ikxk9olb06d3iuf89i3visjck0lpnr0is9glzic04ry.jpeg" caption="Checkout" mode="responsive" height="675" width="1920" %}
{% /image %}

3. Then the user will proceed to the checkout page. Here, they will need to click the '**Verify Your Age**' button

{% image url="https://uploads.developerhub.io/prod/kvAX/2lp6qgbjrtdywdu908unyp3ggvrqx2iaxajjkryvnqdbsgbhc0zzgiateg9pqe8a.jpeg" caption="Personal details" mode="responsive" height="1083" width="1920" %}
{% /image %}

4. The user will then be prompted to perform Yoti Age verification by any of the allowed methods.

{% image url="https://uploads.developerhub.io/prod/kvAX/v14dc6mer8i92vkerei3afw74lkxg0qnx2dmzo201bqn6dt2cm2vguws9jcr72xr.jpeg" caption="Yoti Age Verification" mode="responsive" height="1110" width="1920" %}
{% /image %}

5. Once the user has completed age verification, they will taken back to the checkout page which will show a confirmation message. They will then click the '**Place Order**' button to confirm their order.

{% image url="https://uploads.developerhub.io/prod/kvAX/dxf2j3py5lh13sstk93f71w2329rvcr5gf1asf6uh6ydpaxarmxdhkhuir5w83f5.jpeg" caption="Age verified checkout" mode="responsive" height="1087" width="1920" %}
{% /image %}

---

## Review the results

Head to your WooCommerce admin page. 

- Open the Orders page by going to '**WooCommerce -&gt; Orders**'
- See the '**Age Verification Status**' for each order along with the verification details

{% image url="https://uploads.developerhub.io/prod/kvAX/5jzywhn48dfqj03ehfml03nl2y8rds4tgchtizd2jeflv4uzari38eg29bjx03vw.jpeg" caption="Orders page" mode="responsive" height="547" width="1920" %}
{% /image %}