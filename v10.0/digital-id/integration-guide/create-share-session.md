---
type: page
title: Create a Share session
listed: true
slug: create-share-session
description: 
index_title: Create a Share session
hidden: 
keywords: 
tags: 
---

After initialising the Yoti Identity Client, the next step is to configure your backend application to create a Share session. The Yoti SDKs enable integrators to dynamically create these sessions by defining a session configuration. A unique session would also include a share policy, which is a set of requested attributes or schemes for the sharing process.

## Build a policy

A policy is used to define what attributes are requested from the user. You can use the policy builder to define what attributes are needed.

{% code %}
{% tab language="javascript" title="Node.js" %}
const {
  DigitalIdentityBuilders: {
    PolicyBuilder
  }
} = require('yoti');

const policy = new PolicyBuilder()
    // using a predefined method to add an attribute
    .withFullName()
		.withEmail()
    // if you wish the user to prove it's them by taking a selfie on share
    .withSelfieAuthentication()
    .build();
{% /tab %}
{% tab language="java" %}
Policy policy = Policy.builder()
    // using a predefined method to add an attribute
    .withFullName()
    .withEmail()
    // if you wish the user to prove it's them by taking a selfie on share
    .withSelfieAuthentication(true)
    .build();
{% /tab %}
{% tab language="php" %}
<?php

use Yoti\Identity\Policy\PolicyBuilder;

$policy = (new PolicyBuilder())
    // using a predefined method to add an attribute
    ->withFullName()
  	->withEmail()
    // if you wish the user to prove it's them by taking a selfie on share
    ->withSelfieAuthentication()
    ->build();
{% /tab %}
{% tab language="csharp" %}
YotiPolicy policy = new YotiPolicyBuilder()
  // using a predefined method to add an attribute
  .withFullName()
  .withEmail()
  // if you wish the user to prove it's them by taking a selfie on share
  .withSelfieAuthentication()
	.Build();
{% /tab %}
{% tab language="go" %}
policy := (&digitalidentity.PolicyBuilder{})
	// using a predefined method to add an attribute
	.WithFullName()
	.WithEmail()
	// if you wish the user to prove it's them by taking a selfie on share
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
{% tab language="javascript" title="Node.js" %}
const {
  DigitalIdentityBuilders: {
    ShareSessionNotificationBuilder,
    ShareSessionConfigurationBuilder
  }
} = require('yoti');

const notification = new ShareSessionNotificationBuilder()
		.withUrl("your-webhook-url")
		.withMethod("POST")
		.withHeader("Authorization", "<Bearer_token>") // Optional
		.withVerifiedTls(true) 	// Optional
		.build();

const subject = {
  	subject_id: 'some_subject_id_string',
};

const shareSessionConfig = new ShareSessionConfigurationBuilder()
    .withRedirectUri("/your-callback-url")
    .withPolicy(policy)
    .withSubject(subject)
		.withNotification(notification)
    .build();
{% /tab %}
{% tab language="java" %}
ShareSessionNotification notification = ShareSessionNotification.builder("your-webhook-url")
    .withMethod("POST")
  	.withHeader("Authorization", "<Bearer_token>") // Optional
		.withVerifyTls(true) 	// Optional
    .build();

Map<String, Object> subject = new HashMap<>();
subject.put("subject_id", "some_subject_id_string");

ShareSessionRequest shareSessionConfig = ShareSessionRequest.builder()
  	.withRedirectUri("/your-callback-url")
    .withPolicy(policy)
  	.withSubject(subject)
  	.withNotification(notification)
    .build();
{% /tab %}
{% tab language="php" %}
<?php

use Yoti\Identity\ShareSessionRequestBuilder;

$notification = (new ShareSessionNotificationBuilder())
		->withUrl("your-webhook-url")
		->withMethod("POST")
  	->withHeader("Authorization", "<Bearer_token>") // Optional
  	->withVerifyTls(true) // Optional
		->build();

$subject = (object)[
  'subject_id' => 'some_subject_id_string'
];

$shareSessionConfig = (new ShareSessionRequestBuilder())
  	->withRedirectUri("your-callback-url")
    ->withPolicy($policy)
  	->withSubject($subject)
  	->withNotification($notification)
    ->build();
{% /tab %}
{% tab language="csharp" %}
var notification = new Notification
{
  Headers = { },
  Url = "your-webhook-url",
  Method = "POST",
  VerifyTls = true
};

var subject = new
{
  subject_id = "some_subject_id_string"
};

ShareSessionConfiguration shareSessionConfig = new ShareSessionConfigurationBuilder()
  .WithRedirectUri("/your-callback-url")
  .WithPolicy(policy)
  .WithSubject(subject)
  .WithNotification(notification)
  .Build();
{% /tab %}
{% tab language="go" %}
headers := []byte(`{
	"Authorization": "<Bearer_token>"
}`)

notification := (&digitalidentity.ShareSessionNotification{})
	.WithUrl("your-webhook-url")
  .WithMethod("POST")
	.WithHeaders(headers) // Optional
	.WithVerifyTls(true) 	// Optional
  .Build()

subject := []byte(`{
	"subject_id": "my_subject_id"
}`)
                 
shareSessionConfig := (&digitalidentity.ShareSessionBuilder{})
  .WithRedirectUri("/your-callback-url")
	.WithPolicy(policy)
  .WithSubject(subject)
  .WithNotification(notification)
  .Build()
{% /tab %}
{% /code %}

## Create a Share session

Using the session configuration defined above, you can request the creation of a Share session that will be used by the Yoti Webshare script to generate a Yoti QR.

{% code %}
{% tab language="javascript" title="Node.js" %}
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