---
type: page
title: Launch the user view
listed: true
slug: launch-the-user-view
description: 
index_title: Launch the user view
hidden: 
keywords: 
tags: 
---

In the previous section we saw how to create a session request, which returns:

- Session ID

We then use these to construct a URL which loads the Yoti Client. The URL can be used in the following ways:

- As a link on your webpage
- As a link shared securely with a user
- Within an iFrame on your webpage

{% badge type="info" text="Hint" /%} This is only for sessions where the UI needs to be launched 

{% code %}
{% tab language="http" %}
https://age.yoti.com?sessionId=<sessionId>&sdkId=<sdkId>
{% /tab %}
{% /code %}

{% table widths="" %}
| URL Parameter | Description | 
| ---- | ---- | 
| sessionId | The session ID from the Yoti session create response. | 
| sdkId | This is your SDK ID provided to you by Yoti. | 
{% /table %}

Once the Yoti Client has launched, it will take the user through the age verification flow. The user will be redirected to the specified callback URL on completion of one of the age verification methods.

{% image url="https://res.cloudinary.com/developerhub/image/upload/v1603979234/72728/pbpim3nnb57jegewbhno.png" caption="user view" mode="responsive" height="664" width="1060" %}
{% /image %}

{% html %}
<div class="alert-GTK">
    <div class="alert-title" id="GTK">
        Good to know
    </div>
    <div class="alert-text">
        While it is possible to use this solution in an iFrame, using a new browser window will guarantee an optimal user experience.
    </div>
    <div class="alert-links"> 

   </div>
</div>
{% /html %}

## Preferred method

Yoti offers flexibility when it comes to presenting the user interface of specific methods to end users. If you wish to encourage a particular age verification method to be used first, you can launch the user directly into that specific method. Doing so will mandate the option. If the user fails this method, they can fallback to a different method that has been enabled if retries have been configured. The option to directly launch specific methods also gives integrators the ability to show a list of the methods that they have configured in their own UI.

{% table widths="" %}
| Method | URL | 
| ---- | ---- | 
| Age estimation | [https://age.yoti.com/age-estimation?sessionId=&lt;sessionId&gt;&sdkId=&lt;sdkId](https://age.yoti.com/age-estimation?sessionId=%3CsessionId%3E&amp;sdkId=%3CsdkId)&gt; | 
| IDV | [https://age.yoti.com/doc-scan?sessionId=&lt;sessionId&gt;&sdkId=&lt;sdkId](https://age.yoti.com/doc-scan?sessionId=%3CsessionId%3E&amp;sdkId=%3CsdkId)&gt; | 
| Digital id | [https://age.yoti.com/yoti?sessionId=&lt;sessionId&gt;&sdkId=&lt;sdkId](https://age.yoti.com/yoti?sessionId=%3CsessionId%3E&amp;sdkId=%3CsdkId)&gt; | 
| Credit card | [https://age.yoti.com/credit-card?](https://age.yoti.com/credit-card?%5BsessionId=%3CsessionId%3E&amp;sdkId=%3CsdkId%5D(https://age.yoti.com/yoti?sessionId=%3CsessionId%3E&amp;sdkId=%3CsdkId))[sessionId=&lt;sessionId&gt;&sdkId=&lt;sdkId](https://age.yoti.com/yoti?sessionId=%3CsessionId%3E&amp;sdkId=%3CsdkId)&gt; | 
| Mobile | [https://age.yoti.com/mobile?](https://age.yoti.com/mobile?%5BsessionId=%3CsessionId%3E&amp;sdkId=%3CsdkId%5D(https://age.yoti.com/yoti?sessionId=%3CsessionId%3E&amp;sdkId=%3CsdkId))[sessionId=&lt;sessionId&gt;&sdkId=&lt;sdkId](https://age.yoti.com/yoti?sessionId=%3CsessionId%3E&amp;sdkId=%3CsdkId)&gt; | 
| LA wallet | [https://age.yoti.com/la-wallet?](https://age.yoti.com/la-wallet?%5BsessionId=%3CsessionId%3E&amp;sdkId=%3CsdkId%5D(https://age.yoti.com/yoti?sessionId=%3CsessionId%3E&amp;sdkId=%3CsdkId))[sessionId=&lt;sessionId&gt;&sdkId=&lt;sdkId](https://age.yoti.com/yoti?sessionId=%3CsessionId%3E&amp;sdkId=%3CsdkId)&gt; | 
| Social security number | [https://age.yoti.com/social-security-number?](https://age.yoti.com/social-security-number?%5BsessionId=%3CsessionId%3E&amp;sdkId=%3CsdkId%5D(https://age.yoti.com/yoti?sessionId=%3CsessionId%3E&amp;sdkId=%3CsdkId))[sessionId=&lt;sessionId&gt;&sdkId=&lt;sdkId](https://age.yoti.com/yoti?sessionId=%3CsessionId%3E&amp;sdkId=%3CsdkId)&gt; | 
{% /table %}

#### Age estimation example

Below is an example of initially directing a user to the age estimation method and then giving them the opportunity to select a different method if they failed to meet the age verification threshold.  

{% image url="https://uploads.developerhub.io/prod/kvAX/1ahpc4pqs3fsf27zx12r9duozc0dqm7a1x4kvs5eskbxvftciubn80l3l5emyh9j.png" mode="responsive" height="964" %}
{% /image %}

Once the user attempts the age estimation method but fails to meet the age threshold, they will be presented with the following screen:

{% image url="https://uploads.developerhub.io/prod/kvAX/cfz4bkxy2juqyeoicx672roscmx1bw8rvsp1h4rnhcgonwzr7qo4t1b4q67mlly3.png" mode="responsive" height="1488" %}
{% /image %}

If then they click on the 'Select another method' button they will be presented with the other available methods:

{% image url="https://uploads.developerhub.io/prod/kvAX/s3eh7lf4kl7p6e6rav261wxavvvznlqs8v0v6430px35dlb2hh23u1s2j7vvo4s4.png" mode="responsive" height="1306" %}
{% /image %}

{% callout type="warning" title="Important" %}
retry_enabled must be set to "true" to allow users to try different methods upon failure.
{% /callout %}

---