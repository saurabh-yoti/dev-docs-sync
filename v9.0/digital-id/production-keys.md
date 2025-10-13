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

Before creating your service, you will need to ensure you are logged into [Yoti Hub](https://hub.yoti.com/iam/login) and inside your organisation.

You will then need to create an application to obtain your API keys. You can do this as follows:

- Head to the left hand nav bar and **select services** &gt; **create a service.**
- Or select the blue button labelled **CREATE**.

{% image url="https://uploads.developerhub.io/prod/kvAX/xoaj147vmwc8hf4hn3gh5dhsvedwr76itzmz49ss3cpwf4snppv7ngkboweapi4p.png" mode="responsive" height="542" width="2880" %}
{% /image %}

- Then pick which service you are integrating, in this case - **Digital ID**. 

Each service has a different set-up, so make sure you have selected the correct one. You can create multiple services within your organisation, where in each service refers to a domain and has its own user base.

Once you have selected a service, you can create the service by filling in the following details:

{% image url="https://uploads.developerhub.io/prod/kvAX/mzsf6rm96j433te86q272pegmbfun30sb5dijp4mrtcls2a80h7nhmh7oxtwwe1n.png" mode="responsive" height="1272" width="2040" %}
{% /image %}

{% table widths="" %}
| Form | Description | 
| ---- | ---- | 
| Service name | This will be visible to your users on the Digital ID app. | 
| Internal service name | An internal project name, not visible to your users. | 
| Description | Your service description, which will be shown to users if you choose to integrate the connect QR code only. | 
| Domain | The website domain your service will be used on. Invalid TLDs such as .test or .local are not supported. | 
| Privacy policy | You are legally required to provide information to users on your personal information collection and use practices. This could be through your privacy policy, terms and conditions or another method. | 
| Background image | Your QR code background, which will be shown to users if you choose to integrate the connect QR code only. | 
| Logo | Your logo will be shown in the Digital ID app and also in the receipts generated. Max 200kB file size, PNG only. | 
| Callback URL | Where your clients will be forwarded after the share is completed. | 
{% /table %}

---

## Key Generation

The next stage is to generate SDK ID and the key pair for your service.

{% image url="https://uploads.developerhub.io/prod/kvAX/ac3zzpcctr0lut06eillx4f9owu1h57yajtmmv6v6z69k6iy7gf0n2we59aki5sr.png" mode="responsive" height="864" width="1822" %}
{% /image %}

{% table widths="147" %}
| Key | Description | 
| ---- | ---- | 
| Yoti Client SDK ID | You will need this on your backend to initialise the SDK and it is passed in each call to our servers. | 
| PEM file | You need to download a PEM file containing your private key in order for your app to connect with Yoti.\n\n\n\n• Click the Generate key pair button in the Keys tab to download.\n\n\n\n• Please keep this safe as this PEM file is essential to a Yoti integration.\n\n\n\nIf you lose or corrupt your PEM file you will be able to generate a new one. Regenerating your key pair will break your current application by invalidating your current PEM file and generated keys. This means you will be unable to decrypt new tokens until these are replaced by the newly generated ones. | 
{% /table %}

---

## Scenario Creation

Once the keys have been generated a scenario will need to be created, this is where you can select the attributes that the user will send. When creating a scenario, you will also need to specify a callback url that a user can be redirected to after they have used their digital id.

{% image url="https://uploads.developerhub.io/prod/kvAX/xxigpxgt3cu0ipdyfa5ngiy13ud4fw0mwgp1d87ismvv7ycyyemzacqvjbazqck9.png" mode="responsive" height="1042" width="1832" %}
{% /image %}

---

## Activate your service

Once you have completed the above steps, you will be able to activate your Yoti service by clicking the Activate button in the top right.

{% image url="https://uploads.developerhub.io/prod/kvAX/hppo5t0c018hyazrdg89n2y0ag4othq2br395xhw8rybc7lnk1csv5ke15nxu7jn.png" mode="responsive" height="460" width="2388" %}
{% /image %}

### Continue integration

Once you've onboarded your organisation in Yoti Hub and have generated your API keys, you can continue with integrating your chosen Yoti products or services.

---

## Deleting your application

To delete your service go Services &gt; **Arrow** icon &gt; press **Delete**. 

{% image url="https://uploads.developerhub.io/prod/kvAX/r8enzhxxf7itedkfhy5z9q1kgugpge4dxjcdwygmm1m8hwnbjdvr2uh9o61618ck.png" mode="responsive" height="470" width="2388" %}
{% /image %}

There is also an option to deactivate your service which will keep an archive of your users receipts and integration as a paused state. Users will not be able use your integration until it gets activated again.

{% badge type="info" text="Hint" /%} If you delete your service we cannot recover this for you and you will lose all your user receipts.