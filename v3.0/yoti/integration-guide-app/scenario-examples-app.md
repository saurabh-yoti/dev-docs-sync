---
type: page
title: Scenario examples
listed: true
slug: scenario-examples-app
description: 
index_title: Scenario examples
hidden: 
keywords: 
tags: 
---

In this section you’ll find visual examples of how to present the Yoti SDK. Choose what scenario you want to integrate and follow this recommendation for a better conversion.

{% html %}
<div class="alert-BYS">
   <div class="alert-title" id="BYS">
      Before you start
   </div>
   <div class="alert-text" >
      Make sure you understand how a Yoti integration works by looking at our guide
   </div>
   <div class="alert-links"> 
      <a  target="_self"  href="https://developers.yoti.com/yoti/technical-overview-app">See Integration guide</a>
   </div>
</div>
{% /html %}

## Select your scenario

- [Prove identity](/yoti/scenario-examples-app#prove-identity)
- [Prove age](/yoti/scenario-examples-app#prove-age)
- [Log in / Sign in](/yoti/scenario-examples-app#login)
- [Register / Sign up](/yoti/scenario-examples-app#register)

---

### Prove identity

Customers use the free Yoti app to securely share pre-verified details with your business. Customers only need to verify themselves once using the app.

### Structure

{% image url="https://res.cloudinary.com/developerhub/image/upload/v1575565774/23393/pgigt7mayoiujrcjiya6.jpg" mode="responsive" height="768" width="1354" %}
{% /image %}

### Layouts

It is recommended that the vertical order of the structure above is maintained. For desktop users where horizontal space exists, we recommend separating **How To** from other sections as shown below:

{% image url="https://res.cloudinary.com/developerhub/image/upload/v1574949430/23393/keoxefnbftjjdaozm5ra.jpg" caption="A diagram of our mobile and web best practice for proving the identity." mode="responsive" height="561" width="978" %}
{% /image %}

### Flows

You can choose what data you request from the user, to see what attributes we offer please head [here](https://developers.yoti.com/yoti/knowledge-base-hub#yoti-attributes-explained).

The flow from your site would be similar to this for verify:-

{% image url="https://res.cloudinary.com/developerhub/image/upload/v1593522000/29774/agqfwez2bri9eqnzbpnm.jpg" mode="600" height="714" width="633" %}
{% /image %}

Please note: The technical flow has been simplified, for detail on how the SDK works please visit [here](https://developers.yoti.com/yoti/integration-guide-app#technical-overview).

---

## Prove Age

Customers use the free Yoti app to securely share pre-verified details with your business. Customers only need to verify themselves once using the app.

### Structure

{% image url="https://res.cloudinary.com/developerhub/image/upload/v1575565300/23393/pgxbzqb84v3y6kk0db45.jpg" mode="responsive" height="762" width="1420" %}
{% /image %}

### Layouts

It is recommended that the vertical order of the structure above is maintained. For desktop users where horizontal space exists, we recommend separating **How To** from other sections as shown below:

{% image url="https://res.cloudinary.com/developerhub/image/upload/v1575565343/23393/llh0lofgatpobkkpebl9.jpg" caption="A diagram of our mobile and web best practice for proving age" mode="responsive" height="708" width="1226" %}
{% /image %}

### Flows

You can choose what data you request from the user, to see what attributes we offer please head [here](https://developers.yoti.com/yoti/knowledge-base-hub#yoti-attributes-explained). We recommend:

- Date of birth
- Age_Over - Whether the user is over the specified age, as calculated from their date of birth. Either "true" or "false".

The flow from your site would be similar to this for Age verification:-

{% image url="https://res.cloudinary.com/developerhub/image/upload/v1593522539/29774/fol6r88jhuvm2jn3rp4h.jpg" mode="600" height="885" width="633" %}
{% /image %}

Please note: The technical flow has been simplified,  for detail on how the SDK works please visit [here](https://developers.yoti.com/yoti/integration-guide-app#technical-overview).

---

## Login

Customers logging in with Yoti rely less on guidance to continue. Customers use Yoti to login regularly using the app. It is recommended that you provide a button/link in your page that directs users - wanting to register with Yoti - to the register scenario.

### Structure

{% image url="https://res.cloudinary.com/developerhub/image/upload/v1575565522/23393/emxbfuv8ldtxkxxruo76.jpg" mode="responsive" height="418" width="1332" %}
{% /image %}

### Layouts

It is recommended that the vertical order of the structure above is maintained across all devices.

{% image url="https://res.cloudinary.com/developerhub/image/upload/v1575565557/23393/jvkwoveueul5ynfydng1.jpg" caption="A diagram of our mobile and web best practice for login." mode="responsive" height="698" width="1212" %}
{% /image %}

---

## Register

Customers registering using Yoti rely on guidance to continue. Customers only need to verify themselves once using the app. It is recommended that you provide a button/link in your login page, that directs users wanting to register with Yoti, to this scenario.

### Structure

{% image url="https://res.cloudinary.com/developerhub/image/upload/v1575565617/23393/ux8bdir8tch8qkh930tt.jpg" mode="responsive" height="754" width="1372" %}
{% /image %}

### Layouts

It is recommended that the vertical order of the structure above is maintained. For desktop users where horizontal space exists, we recommend separating **How To** from other sections as shown below:

{% image url="https://res.cloudinary.com/developerhub/image/upload/v1575565655/23393/wicccsmwtluwok8hghnf.jpg" caption="A diagram of our mobile and web best practice for registration" mode="responsive" height="688" width="1222" %}
{% /image %}

### Flows (Register and Login)

You can choose what data you request from the user, to see what attributes we offer please head [here](https://developers.yoti.com/yoti/knowledge-base-hub#yoti-attributes-explained). We recommend using the attribute: [Remember Me ID](https://developers.yoti.com/yoti/knowledge-base-hub#remember-me-id-explained) when handling registration and login flow.  

The flow from your site would be similar to this for Age verification:-

{% image url="https://res.cloudinary.com/developerhub/image/upload/v1593524320/29774/bvdfpal199jnudevjzzf.jpg" mode="responsive" height="1509" width="636" %}
{% /image %}

Please note: The technical flow has been simplified, for detail on how the SDK works please visit [here](https://developers.yoti.com/yoti/integration-guide-app#technical-overview).