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

To create your service you will need to ensure you are logged into the hub and inside your organisation.

You will need to create an service in the hub to obtain your API keys. You can do this two ways either:

- Head to the left hand nav bar and **select service** &gt; **create a service.**
- Or select the blue button labelled **CREATE**.

{% image url="https://uploads.developerhub.io/prod/kvAX/6cr9c7h0155tq5cntekn35rh86t3rj2f7gldj6n42jjn3a17tcd18m4gr8g8tftj.png" mode="responsive" height="408" width="2878" %}
{% /image %}

- Then pick which product you are integrating, in this case - **Age verification**. So select **Age checks** &gt; **Age** **verification.**

{% image url="https://uploads.developerhub.io/prod/kvAX/zf54w7c6fjdvq8w7awnektluv6i4lnosk4t09phbfnzgzc3m4s261k8yukaggzcq.png" mode="responsive" height="1068" width="1798" %}
{% /image %}

---

## Key generation

The next stage is to collect various IDs for your service.

{% image url="https://uploads.developerhub.io/prod/kvAX/17uxopc92hmxxgbw29s5pcg965otetp0j8jl9va5hqssol8pktxcu4dhx28kw04k.png" caption="Generating keys and settings" mode="responsive" height="931" width="940" %}
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

{% image url="https://uploads.developerhub.io/prod/kvAX/whd7ge9y9lcqlacdz3ej0ws8ngzu7r0bv82iw74l4h27st18ekmi6kohoyzvkywx.jpg" caption="Deleting your service" mode="responsive" height="366" width="1628" %}
{% /image %}

{% badge type="info" text="Hint" /%} If you delete your service we cannot recover this for you.