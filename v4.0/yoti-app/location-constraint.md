---
type: page
title: Location constraint
listed: true
slug: location-constraint
description: 
index_title: Location constraint
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
      Get familiar with our Dynamic QR code.
   </div>
   <div class="alert-links"> 
      <a  target="_self" href="https://developers.yoti.com/yoti-app/generate-the-button#dynamic-qr"> Dynamic QR code </a>
   </div>
</div>
{% /html %}

Adding an extension to a scenario adds some enhanced behaviour to the Yoti app when scanning a QR code.

This extension allows the integrator to provide an expected location area where the device should be when doing the share. During the share completion the location information in the QR code are used to validate the device location. Given the accuracy of the device location, the expected location area must include a maximum uncertainty radius, above which the share will be rejected. The share will be cancelled if the device is not within the expected location.

{% code %}
{% tab language="javascript" %}
const locationExtension = new Yoti.LocationConstraintExtensionBuilder()
    .withLatitude(51.5074)
    .withLongitude(-0.1278)
    .withRadius(6000)
		.withMaxUncertainty(6000)
    .build();
{% /tab %}
{% tab language="java" %}
Extension<LocationConstraintContent> locationExtension = new SimpleLocationConstraintExtensionBuilder()
                .withLatitude(51.5074)
                .withLongitude(-0.1278)
                .withRadius(6000)
  							.withMaxUncertainty(6000)
                .build();
{% /tab %}
{% /code %}

{% table %}
| Parameter | Units | Description | 
| ---- | ---- | ---- | 
| Latitude | decimal degrees | Device's latitude | 
| Longitude | decimal degrees | Device's longitude | 
| Radius | meters | Radius of the circle centred on the specified location coordinates where the device is allowed to perform the share. (Default 150) | 
| Max Uncertainty | meters | Maximum acceptable length of the radius representing the area of uncertainty associated with the device location coordinates. (Default 150) | 
{% /table %}

{% code %}
{% tab language="javascript" %}
Javascript
const dynamicScenario = new Yoti.DynamicScenarioBuilder()
      .withCallbackEndpoint("/your-callback")
      .withPolicy(dynamicPolicy)
      //if using an extension
      .withExtension(Locationextension)
      .build();
Copy
{% /tab %}
{% /code %}