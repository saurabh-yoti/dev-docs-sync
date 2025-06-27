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

You will need to create an service in the hub to obtain your API keys. You can do this two ways either:

- Head to the left hand nav bar and **select Services** &gt; C**reate a service.**
- Or select the blue button labelled **CREATE**.

{% image url="https://uploads.developerhub.io/prod/kvAX/zhedcu0j2xmfxxfsgdlqrw3suwq2kfvs5xo5y6xcc0ahl39ks711scnqfi1g4fg0.png" mode="responsive" height="408" width="2878" %}
{% /image %}

- Pick which product you are integrating, in this case - **Age checks**.

{% image url="https://uploads.developerhub.io/prod/kvAX/wokcs57cst59rb6846vfe5b7yr53ul205sga16w8e32ll4e9ne48c9i96ex5xqni.png" mode="responsive" height="1428" width="2398" %}
{% /image %}

- Then select the **Age verification** option.

{% image url="https://uploads.developerhub.io/prod/kvAX/tupdo942hw1dw4naazyydcvx0ssy2mgdgl5c2uehijob6mjxqvtv4lbimm76bme8.png" mode="responsive" height="1218" width="2398" %}
{% /image %}

- Specify the service name and click on 'CREATE'.

{% image url="https://uploads.developerhub.io/prod/kvAX/5oq6bi63qm22pa2bp0eujkqocgkks8iu6d7ltkpo28tgkq0p2wyxhg3zvb64mymx.png" caption="Create an Age verification service" mode="responsive" height="1192" width="2398" %}
{% /image %}

---

## Key generation

The next stage is to collect various IDs for your application.

{% image url="https://res.cloudinary.com/developerhub/image/upload/v1639911985/v2_2762/ppjjd7eniejekaveooeg.png" caption="Generating keys and settings" mode="set" height="741.828125" width="749" %}
{% /image %}

If you want to add premium services please tick the boxes in the blue box to enable. You can always change this later.

{% table widths="147" %}
| Key | Description | 
| ---- | ---- | 
| Yoti Client SDK ID | You will need this on your backend to initialise the API and it is passed in each call to our servers. | 
| API Key | The age verification API uses an HTTP authentication scheme called ‘bearer authentication’. This involves security tokens called ‘bearer tokens’. They are the predominant type of access token used with [OAuth 2.0](https://oauth.net/2/). A resource should interpret a bearer token as "Give the bearer of this token access". The client must send this token in the Authorization header when making requests to protected resources. | 
{% /table %}

---

## Continue integration

Once you've onboarded your organisation in Yoti Hub and have generated your API keys, you can continue with integrating your chosen Yoti products or services.

---

## Deleting your service

To delete your service go Service &gt; **Edit** button &gt; press **Delete**.

There is also an option to deactivate your service which will hold your integration as a paused state. Users will not be able use your integration until it gets activated again.

{% image url="https://res.cloudinary.com/developerhub/image/upload/v1575294779/20476/er1ipudlofoajnrvny7t.jpg" caption="Deleting your application" mode="responsive" height="366" width="1628" %}
{% /image %}

{% badge type="info" text="Hint" /%} If you delete your service we cannot recover this for you.