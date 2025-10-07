---
type: page
title: Production keys
listed: true
slug: production-keys
description: 
index_title: Production keys
hidden: 
keywords: 
tags: 
---

To create your application you will need to ensure you are logged into the hub and inside your organisation.

You will need to create a service in the hub to obtain your API keys. You can do this two ways either:

- Head to the left hand nav bar and **select services** &gt; **create a service.**
- Or select the blue button labelled **CREATE**.

{% image url="https://uploads.developerhub.io/prod/kvAX/2bhj779qmzon2i14j14os59gncc2ucl9emjd289nf0d78tllhs8o2si80iqi2ujs.png" mode="responsive" height="366" width="2874" %}
{% /image %}

- Then pick which product you are integrating, in this case - **Identity verification**. 

Each service has a different set up. Organisations at Yoti are set up in the following way:

You can create multiple services within your organisation, each service refers to a domain and has its own user base.

{% image url="https://uploads.developerhub.io/prod/kvAX/8gj6q0zyj6hvl5vuhm56enw3u8z17rkhwnn0odmc1rd70cclegx965qr99hxrnk9.png" mode="responsive" height="1156" width="2056" %}
{% /image %}

---

## Key Generation

The next stage is to collect various IDs and the key pair for your service.

{% image url="https://uploads.developerhub.io/prod/kvAX/9qisfejl3dtjl5xkin8dxyllsmm5a0hu81a8zvj12leoojoi0xm4vyudexhs9p9v.png" mode="responsive" height="1102" width="2084" %}
{% /image %}

If you want to enable seeing sessions in the portal then please ensure you click the box to enable the user of portal.

If you do not want to view your sessions in the portal just tick the notes section.

{% image url="https://image-archive.developerhub.io/image/upload/v2_2762/yvmik5hxlnrlhoxfcys8/1639922214.png" caption="Generating keys and PEM file for portal too" mode="responsive" height="659" width="595" %}
{% /image %}

{% table widths="147" %}
| Key | Description | 
| ---- | ---- | 
| Yoti Client SDK ID | You will need this on your backend to initialise the SDK and it is passed in each call to our servers. | 
| Pem file | You need to download a PEM file containing your private key in order for your app to connect with Yoti.\n\n\n\n• Click the Generate key pair button in the Keys tab to download.\n\n\n\n• Please keep this safe as this PEM file is essential to a Yoti integration.\n\n\n\nIf you lose or corrupt your PEM file you will be able to generate a new one. Regenerating your key pair will break your current service by invalidating your current PEM file and generated keys. This means you will be unable to decrypt new tokens until these are replaced by the newly generated ones. | 
{% /table %}

---

## Activate your service

Once you have completed the above steps, you will be able to activate your Yoti service by clicking the Activate button in the top right.

{% image url="https://uploads.developerhub.io/prod/kvAX/n49xbfrbej6u0h1w1dkht642h25r0zhyevwv3f4fmj8iarrlw8ogzzgkiur3p40w.png" mode="responsive" height="788" width="2398" %}
{% /image %}

### Continue integration

Once you've onboarded your organisation in Yoti Hub and have generated your API keys, you can continue with integrating your chosen Yoti products or services.

---

## Deleting your services

To delete your service go Services &gt; **Arrow** icon &gt; press **Delete**. 

{% image url="https://uploads.developerhub.io/prod/kvAX/ifi7stub4nyd4waiff0gmgt2fr2sjzvvdmeunuu2qmb2873w589y9uyr8cluazlk.png" mode="responsive" height="862" width="2394" %}
{% /image %}

There is also an option to deactivate your service which will hold your integration as a paused state. Users will not be able use your integration until it gets activated again.

{% badge type="info" text="Hint" /%} If you delete your service we cannot recover this for you.