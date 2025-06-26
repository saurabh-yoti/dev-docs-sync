---
type: page
title: Production Keys
listed: true
slug: production-keys
description: 
index_title: Production Keys
hidden: 
keywords: 
tags: 
---


To create your application you will need to ensure you are logged into the hub and inside your organisation.

You will need to create an application in the hub to obtain your API keys. You can do this two ways either:

- Head to the left hand nav bar and **select application** &gt; **create an application.**
- Or select the blue button labelled **CREATE**.


{% image url="https://uploads.developerhub.io/prod/kvAX/qki9mnh1x7hgxkynx4s5gs79moh95a13lpnjhof1u9tu4cej8bigjp39jbkq0ti3.png" caption="" mode="responsive" height="548" width="3076" %}
{% /image %}


- Then pick which product you are integrating, in this case - **Identity verification**.

Each service has a different set up. Organisations at Yoti are set up in the following way:

You can create multiple applications within your organisation, each application refers to a domain and has its own user base.


{% image url="https://uploads.developerhub.io/prod/kvAX/2sa05ddrvcwiuvqx10j1ojalhamcbqd74zeal58ej0e5atxy7143pljgyujgc097.png" caption="Create a Identity verification application" mode="responsive" height="1180" width="2060" %}
{% /image %}


---

## Key Generation

The next stage is to collect various IDs and the key pair for your application.


{% image url="https://uploads.developerhub.io/prod/kvAX/p6t9lm3z97om4eclgshh4rhuwoprebw2u0gigkihvcm69hdysq5f1gv9ljfx15t4.jpg" caption="Generating keys and PEM file" mode="responsive" height="1126" width="1884" %}
{% /image %}


If you want to enable seeing sessions in the portal then please ensure you click the box to enable the user of portal.

If you do not want to view your sessions in the portal just tick the notes section.


{% image url="https://uploads.developerhub.io/prod/kvAX/3vb2d911gkngmnny0gu70o6htrm7dp44sdgyanzogvbes5k3ciq9pgqxj8u54fng.png" caption="Generating keys and PEM file for portal too" mode="responsive" height="659" width="595" %}
{% /image %}



{% table widths="147" %}
| Key | Description | 
| ---- | ---- | 
| Yoti Client SDK ID | You will need this on your backend to initialise the SDK and it is passed in each call to our servers. | 
| Pem file | You need to download a PEM file containing your private key in order for your app to connect with Yoti.\n\n\n\n• Click the Generate key pair button in the Keys tab to download.\n\n\n\n• Please keep this safe as this PEM file is essential to a Yoti integration.\n\n\n\nIf you lose or corrupt your PEM file you will be able to generate a new one. Regenerating your key pair will break your current application by invalidating your current PEM file and generated keys. This means you will be unable to decrypt new tokens until these are replaced by the newly generated ones. | 
{% /table %}


---

## Activate your application

Once you have completed the above steps, you will be able to activate your Yoti application by clicking the Activate button in the top right.


{% image url="https://uploads.developerhub.io/prod/kvAX/oaefxv1uofgsx3nw9lp8vpvk9zuqq8tk6h7680qbznvrfpeg8cwndiyg6dv97kby.jpg" caption="Activating your application" mode="600" height="536" width="1748" %}
{% /image %}


### Continue integration

Once you've onboarded your organisation in Yoti Hub and have generated your API keys, you can continue with integrating your chosen Yoti products or services.

---

## Deleting your application

To delete your application go Application &gt; **Edit** button &gt; press **Delete**.


{% image url="https://uploads.developerhub.io/prod/kvAX/8ichvykm4up24vjzm842iv6j5119trr4ug46ka5vkozg5gypj5zorei8rweq84vm.jpg" caption="Deleting your application" mode="responsive" height="366" width="1628" %}
{% /image %}


There is also an option to deactivate your application which will hold your integration as a paused state. Users will not be able use your integration until it gets activated again.

{% badge type="info" text="Hint" /%} If you delete your application we cannot recover this for you.

