---
type: page
title: Request the credential
listed: true
slug: request-the-credential
description: 
index_title: Request the credential
hidden: 
keywords: 
tags: 
---

You will then need to generate a QR code to retrieve the newly-issued credential. The share result will contain the QR code URL to present the dynamic QR code.

{% code %}
{% tab language="javascript" %}
const dynamicPolicy = new DynamicPolicyBuilder()
    .withWantedAttributeByName('com.example.someAttribute')
    .build();

const dynamicScenario = (new DynamicScenarioBuilder())
    .withCallbackEndpoint('/account/connect')
    .withPolicy(dynamicPolicy)
    .build();

const shareUrlResult = yotiClient.createShareUrl(dynamicScenario);
{% /tab %}
{% tab language="java" %}
DynamicPolicy dynamicPolicy = DynamicPolicy.builder()
    .withWantedAttribute(false, "com.example.someAttribute")
    .build();
 
DynamicScenario dynamicScenario = DynamicScenario.builder()
    .withCallbackEndpoint("/account/connect")
    .withPolicy(dynamicPolicy)
    .build();
{% /tab %}
{% tab language="php" %}
<?php

use Yoti\ShareUrl\DynamicScenarioBuilder;
use Yoti\ShareUrl\Policy\DynamicPolicyBuilder;

$dynamicPolicy = (new DynamicPolicyBuilder())
    ->withWantedAttributeByName('com.example.someAttribute')
    ->build();

$dynamicScenario = (new DynamicScenarioBuilder())
    ->withCallbackEndpoint('/account/connect')
    ->withPolicy($dynamicPolicy)
    ->build();

$shareUrlResult = $yotiClient->createShareUrl($dynamicScenario)->getShareUrl();
{% /tab %}
{% tab language="python" %}
from yoti_python_sdk import Client

from yoti_python_sdk.dynamic_sharing_service import (
    create_share_url,
    DynamicScenarioBuilder,
)

from yoti_python_sdk.dynamic_sharing_service.policy.dynamic_policy_builder import (
    DynamicPolicyBuilder,
)

client = Client("CLIENT_SDK_ID", "/path/to/key.pem")

policy = (
    DynamicPolicyBuilder()
    .with_wanted_attribute_by_name("com.example.someAttribute")
    .build()
)

scenario = (
    DynamicScenarioBuilder()
    .with_callback_endpoint("/account/connect")
    .with_policy(policy)
    .build()
)

share_url_result = share = create_share_url(client, scenario)
{% /tab %}
{% tab language="csharp" %}
DynamicPolicy dynamicPolicy = new DynamicPolicyBuilder()
   .WithWantedAttribute(_thirdPartyAttributeName)
   .Build();

DynamicScenario dynamicScenario = new DynamicScenarioBuilder()
	.WithCallbackEndpoint("/account/connect")
	.WithPolicy(dynamicPolicy)
	.Build();

ShareUrlResult shareUrlResult = yotiClient.CreateShareUrl(dynamicScenario);
{% /tab %}
{% tab language="go" %}
policy, err := (&dynamic.PolicyBuilder{}).
	WithWantedAttributeByName("com.example.someAttribute").
	Build()

if err != nil {
	panic(err)
}

var scenario dynamic.Scenario
scenario, err = (&dynamic.ScenarioBuilder{}).
	WithCallbackEndpoint("/account/connect").
	WithPolicy(policy).
	Build()

if err != nil {
	panic(err)
}

var shareUrlResult dynamic.ShareURL
shareUrlResult, err = client.CreateShareURL(&scenario)
{% /tab %}
{% tab language="ruby" %}
policy = Yoti::DynamicSharingService::DynamicPolicy
         .builder
         .with_wanted_attribute_by_name('com.example.someAttribute')
         .build

scenario = Yoti::DynamicSharingService::DynamicScenario
           .builder
           .with_callback_endpoint('/account/connect')
           .with_policy(policy)
           .build

share_url_result = Yoti::DynamicSharingService.create_share_url(scenario)
{% /tab %}
{% /code %}

To generate your dynamic QR code on your front end you will need the shareURL and SDK ID from your application.