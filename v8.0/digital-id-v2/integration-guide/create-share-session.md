---
type: page
title: Create Share session
listed: true
slug: create-share-session
description: 
index_title: Create Share session
hidden: 
keywords: 
tags: 
---

After initialising the Yoti Identity Client, the next step is to configure your backend application to create a Share session. The Yoti SDKs enable integrators to dynamically create these sessions by defining a session configuration. A unique session would also include a share policy, which is a set of requested attributes or schemes for the sharing process.

## Build a policy

A policy is used to define what attributes are requested from the user. You can use the policy builder to define what attributes are needed.

{% code %}
{% tab language="javascript" %}
const requirements = {
  trust_framework: 'UK_TFIDA',
  scheme: {
    type: 'DBS_RTW',
    objective: 'STANDARD',
  }
};

const policy = new Yoti.PolicyBuilder()
		// Optional - if you wish to carry out DBS and/or RTW check
    .withIdentityProfileRequirements(requirements)
    //using a predefined method to add an attribute
    .withFullName()
		.withEmail()
    //if you wish the user to prove it's them by taking a selfie on share
    .withSelfieAuthentication()
    .build();
{% /tab %}
{% tab language="java" %}
JSONObject scheme = new JSONObject();
scheme.put("type", "DBS_RTW");
scheme.put("objective", "STANDARD");

JSONObject requirements = new JSONObject();
requirements.put("trust_framework", "UK_TFIDA");
requirements.put("scheme", scheme);

Policy policy = Policy.builder()
  	// Optional - if you wish to carry out DBS and/or RTW check
  	.withIdentityProfile(requirements)
    //using a predefined method to add an attribute
    .withFullName()
    .withEmail()
    //if you wish the user to prove it's them by taking a selfie on share
    .withSelfieAuthentication(true)
    .build();
{% /tab %}
{% tab language="php" %}
<?php

use Yoti\Identity\Policy\PolicyBuilder;

$requirements = (object)[
  'trust_framework' => 'UK_TFIDA',
  'scheme' => [
    'type' => 'DBS_RTW',
    'objective' => 'STANDARD'
  ]
];


$policy = (new PolicyBuilder())
 		// Optional - if you wish to carry out DBS and/or RTW check
		->withIdentityProfileRequirements($requirements)
    //using a predefined method to add an attribute
    ->withFullName()
  	->withEmail()
    //if you wish the user to prove it's them by taking a selfie on share
    ->withSelfieAuthentication()
    ->build();
{% /tab %}
{% tab language="csharp" %}
var requirements = new { 
	trust_framework = "UK_TFIDA",
	scheme = new
	{
		type = "DBS_RTW",
		objective = "ENHANCED"
	}
};

YotiPolicy policy = new YotiPolicyBuilder()
  // if you wish to carry out DBS and/or RTW check
	.WithIdentityProfileRequirements(requirements)
  .withFullName()
  .withEmail()
  // if you wish the user to prove it's them by taking a selfie on share
  .withSelfieAuthentication()
	.Build();
{% /tab %}
{% tab language="go" %}
policy := (&digitalidentity.PolicyBuilder{})
	//using a predefined method to add an attribute
	.WithFullName()
	.WithEmail()
	//if you wish the user to prove it's them by taking a selfie on share
	.WithSelfieAuth()
	.Build()
{% /tab %}
{% /code %}

## Specify the Session configuration

The Session configuration is built using:

- The policy.
- The redirect URI for share completion. This is where the user will be redirected to after the share is completed. A receiptId query parameter will be added to the URL. You can use this to retrieve the user profile from the share.
- A subject Id (optional).
- A notification webhook (optional).
- Any extensions.

{% code %}
{% tab language="javascript" %}
const subject = {
  	subject_id: 'some_subject_id_string',
};

const notification = new Yoti.ShareSessionNotificationBuilder()
		.withUrl("notification-webhook")
		.withMethod("POST")
		.build();

const shareSessionConfig = new Yoti.ShareSessionConfigurationBuilder()
    .withRedirectUri("/your-callback")
    .withPolicy(policy)
    .withSubject(subject)
		.withNotification(notification)
    .build();
{% /tab %}
{% tab language="java" %}
Map<String, Object> subject = new HashMap<>();
subject.put("subject_id", "some_subject_id_string");

ShareSessionNotification notification = ShareSessionNotification.builder("notification-webhook")
    .withMethod("POST")
    .build();

ShareSessionRequest shareSessionConfig = ShareSessionRequest.builder()
  	.withRedirectUri("/your-callback")
    .withPolicy(policy)
  	.withSubject(subject)
  	.withNotification(notification)
    .build();
{% /tab %}
{% tab language="php" %}
<?php

use Yoti\Identity\ShareSessionRequestBuilder;

$subject = (object)[
  'subject_id' => 'some_subject_id_string'
];

$notification = (new ShareSessionNotificationBuilder())
		->withUrl("notification-webhook")
		->withMethod("POST")
		->build();

$shareSessionConfig = (new ShareSessionRequestBuilder())
  	->withRedirectUri("your-callback")
    ->withPolicy($policy)
  	->withSubject($subject)
  	->withNotification($notification)
    ->build();
{% /tab %}
{% tab language="csharp" %}
var subject = new {
	subject_id = "some_subject_id_string"
};

var notification = new ShareSessionNotificationBuilder()
  .WithUrl("notification-webhook")
  .WithMethod("POST")
  .Build();

ShareSessionConfiguration shareSessionConfig = new ShareSessionConfigurationBuilder()
  .WithRedirectUri("/your-callback-url")
  .WithPolicy(policy)
  .WithSubject(subject)
  .WithNotification(notification)
  .Build();
{% /tab %}
{% tab language="go" %}
subject := []byte(`{
	"subject_id": "my_subject_id"
}`)

notification := (&digitalidentity.ShareSessionNotification{})
	.WithUrl("notification-webhook")
  .WithMethod("POST")
  .Build()     
                 
shareSessionConfig := (&digitalidentity.ShareSessionBuilder{})
  .WithRedirectUri("/your-callback-url")
	.WithPolicy(policy)
  .WithSubject(subject)
  .WithNotification(notification)
  .Build()
{% /tab %}
{% /code %}

## Create the Share session

Using the session configuration defined above, you will request the creation of a Share session that will be used by the Yoti Webshare script to generate a Yoti QR.

{% code %}
{% tab language="javascript" %}
yotiClient.createShareSession(shareSessionConfig)
  .then((shareSessionResult) => {
  	const shareSession = shareSessionResult;
  	const shareSessionId = shareSession.getId();
  }).catch((error) => {
    console.error(error.message);
  });
{% /tab %}
{% tab language="java" %}
try {
  	ShareSession shareSession = client.createShareSession(shareSessionConfig);
  	String shareSessionId = shareSession.getId();
} catch (DigitalIdentityException e) {
  	LOG.error(e.getMessage());
}
{% /tab %}
{% tab language="php" %}
<?php

use Yoti\Exception\DigitalIdentityException;

try {
  	$shareSession = $client->createShareSession($shareSessionConfig);
  	$shareSessionId = $shareSession->getId();
} catch (DigitalIdentityException e) {
  	throw new DigitalIdentityException($e->getMessage());
}
{% /tab %}
{% tab language="csharp" %}
ShareSession shareSession = yotiClient.CreateShareSession(shareSessionConfig);
var shareSessionId = shareSession.Id;
{% /tab %}
{% tab language="go" %}
shareSession, err := client.CreateShareSession(shareSessionConfig)
shareSessionId := shareSession.Id
{% /tab %}
{% /code %}