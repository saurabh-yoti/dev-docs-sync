---
type: page
title: Request attributes
listed: true
slug: request-attributes
description: 
index_title: Request attributes
hidden: 
keywords: 
tags: 
---

There are several type of attributes that can be stored on a user's Digital ID app. Yoti provides the ability to request these attributes by specifying a share [policy](https://developers.yoti.com/digital-id/create-share-session#build-a-policy).

The attributes are independent of each other, so they can be requested separately. In order to request the required attributes using our SDKs, see the following examples:

{% code %}
{% tab language="javascript" title="Node.js" highlightLines="" %}
const {
  DigitalIdentityBuilders: {
    PolicyBuilder
  }
} = require('yoti');

const policy = new PolicyBuilder()
    // using predefined methods to request attributes
    .withFullName()
		.withEmail()
    .withPhoneNumber()
		.withPostalAddress()
    .withSelfie()
    .withAgeOver(18)
  	.withDateOfBirth()
    .withNationality()
    .withGender()
		.withStructuredPostalAddress()
    .withDocumentDetails()
    .withDocumentImages()
    .withWantedRememberMe()
		// using attributes specified by name
    .withWantedAttributeByName("given_names")
    .withWantedAttributeByName("family_name")
    // if you wish the user to prove it's them by taking a selfie on share
    .withSelfieAuthentication()
    .build();
{% /tab %}
{% tab language="java" %}
Policy policy = Policy.builder()
    // using predefined methods to request attributes
    .withFullName()
    .withEmail()
  	.withPhoneNumber()
  	.withPostalAddress()
  	.withSelfie()
  	.withAgeOver(18)
  	.withDateOfBirth()
  	.withNationality()
  	.withGender()
  	.withStructuredPostalAddress()
  	.withWantedRememberMe(true)
		// using attributes specified by name
  	.withWantedAttribute(true,"given_names")
  	.withWantedAttribute(true,"family_name")
    // if you wish the user to prove it's them by taking a selfie on share
    .withSelfieAuthentication(true)
    .build();
{% /tab %}
{% tab language="php" %}
<?php

use Yoti\Identity\Policy\PolicyBuilder;

$policy = (new PolicyBuilder())
    // using predefined methods to request attributes
    ->withFullName()
  	->withEmail()
  	->withPhoneNumber()
  	->withPostalAddress()
  	->withSelfie()
  	->withAgeOver(18)
  	->withDateOfBirth()
  	->withNationality()
  	->withGender()
  	->withStructuredPostalAddress()
  	->withDocumentDetails()
  	->withDocumentImages()
  	->withWantedRememberMe(true)
  	// using attributes specified by name
    ->withWantedAttributeByName("given_names")
    ->withWantedAttributeByName("family_name")
    //if you wish the user to prove it's them by taking a selfie on share
    ->withSelfieAuthentication()
    ->build();
{% /tab %}
{% tab language="python" %}
# Coming soon
{% /tab %}
{% tab language="csharp" %}
YotiPolicy policy = new YotiPolicyBuilder()
  	// using predefined methods to request attributes
  	.withFullName()
    .withEmail()
    .WithPhoneNumber()
  	.WithPostalAddress()
    .WithSelfie()
    .WithAgeOver(18)
  	.WithDateOfBirth()
    .WithNationality()
    .WithGender()
		.WithStructuredPostalAddress()
    .WithDocumentDetails()
    .WithDocumentImages()  
  	.WithRememberMeId(true)
    // using attributes specified by name
    .WithWantedAttributeByName("given_names")
    .WithWantedAttributeByName("family_name")
    // if you wish the user to prove it's them by taking a selfie on share
    .withSelfieAuthentication()
    .Build();
{% /tab %}
{% tab language="go" %}
policy := (&digitalidentity.PolicyBuilder{})
    // using a predefined method to add an attribute
    .WithFullName()
    .WithEmail()
		.WithPhoneNumber()
		.WithPostalAddress()
    .WithSelfie()
    .WithAgeOver(18)
  	.WithDateOfBirth()
    .WithNationality()
    .WithGender()
		.WithStructuredPostalAddress()
    .WithDocumentDetails()
    .WithDocumentImages()
    .WithWantedRememberMe()
    // using attributes specified by name
    .withWantedAttributeByName("given_names")
    .withWantedAttributeByName("family_name")
    // if you wish the user to prove it's them by taking a selfie on share
    .WithSelfieAuth()
    .Build()
{% /tab %}
{% /code %}

After creating the policy, you have to specify it in the session configuration as described [here](https://developers.yoti.com/digital-id/create-share-session#specify-the-session-configuration).