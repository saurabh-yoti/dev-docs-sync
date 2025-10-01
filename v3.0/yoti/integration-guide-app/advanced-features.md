---
type: page
title: Advanced Features
listed: true
slug: advanced-features
description: 
index_title: Advanced Features
hidden: 
keywords: 
tags: 
---

## Advanced QR codes

Yoti offers a numerous amount of ways to integrate the Yoti QR code via a Yoti button. This section describes the process of integrating the advanced QR codes we offer:

- [Static QR](https://developers.yoti.com/yoti/advanced-features#static-qr)
- [Non Browser QR](https://developers.yoti.com/yoti/advanced-features#non-browser-qr)
- [Dynamic QR](https://developers.yoti.com/yoti/advanced-features#dynamic-qr)

{% html %}
<div class="alert-BYS">

   <div class="alert-title" id="BYS">

      Before you start

   </div>

   <div class="alert-text" >

   Have a read of our web integration guide and ensure you have onboarded with Yoti and got your API keys.

   </div>

   <div class="alert-links"> 

         <a href="https://developers.yoti.com/yoti/web-integration">Web integration</a>
  <a href="https://developers.yoti.com/yoti/getting-started-hub">Onboarding with Yoti</a>


   </div>

</div>
{% /html %}

### Static QR

A static QR code has no expiry to reload the QR code. Dynamic QR codes have an expiry of 3 minutes until a reload is required. This provides a low cost/offline verification that users can print out and use as many times as needed. Data sent via a static QR code can be viewed in the hub as a [receipt](https://developers.yoti.com/yoti/knowledge-base-hub#customer-receipts). 

An example of a Static QR code is located here: [https://yoti.world/qr-codes/](https://yoti.world/qr-codes/)

The process is:

1. Create an organisation on the hub.
2. [Create an application](https://developers.yoti.com/yoti/generate-api-keys) on the hub and add your scenario. 
3. Send your SDK ID to [sdksupport@yoti.com.](mailto:sdksupport@yoti.com)

We aim to get your QR code to you in 3-4 working days. 

---

### Non Browser QR

This section below describes the process of creating a personalised client which triggers the Yoti QR flow. 

It is possible to manually construct this QR code as this can be necessary in cases where you do not have access to a Web server on your front end, for example using a kiosk of GUI.

Requesting a QR code is broken down into the following steps:

1. Requesting a QR code from Yoti Servers
2. Rending the QR code
3. Decoding and resolving the QR code metadata
4. Opening a web socket channel to Yoti using the resolved metadata
5. Receiving a Yoti token over the web socket channel or handling a session error
6. Passing the received token to the callback url that has been specified in Yoti Hub

**Request a QR code**

In order to request a QR code from Yoti Servers the client must create a `GET HTTPS` request to the following **`Retrieve a QR Code`**endpoint:

{% table %}
| Retrieve a QR code endpoint | 
| ---- | 
| [https://api.yoti.com/api/v1.1/sessions/apps/](https://api.yoti.com/api/v1.1/sessions/apps/)/scenarios/ | 
{% /table %}

{% table %}
| Parameter | Description | 
| ---- | ---- | 
| sdkId | sdkId is the SDK_ID found with your Yoti Hub Application | 
| scenarioId | scenarioId is  the Scenario ID found within your Yoti Hub Application that relates to a specific scenario | 
{% /table %}

A Yoti QR code contains a URL and is returned in full from the `Retrieve a QR code` endpoint.

An example of how a URL in a QR code should look is as follows:

{% code %}
{% tab language="markup" %}
https://code.yoti.com/CAEaJDlhMzg5MTRiLTg0ZDAtNGI3Zi05NDNiLWQzNzBmNmM3YTVlYzAA
{% /tab %}
{% /code %}

{% html %}
<div class="alert-GTK">

    <div class="alert-title" id="GTK">

        Good to know... 

    </div>

    <div class="alert-text">

The important section of the URL is the string that follows https://code.yoti.com/. This is a base 64 url encoded Protocol Buffer.

    </div>

</div>
{% /html %}

**Rendering a Yoti QR Code**

This URL must be transformed into a QR code before it can be scanned with the Yoti app. Yoti provides a simple API to transform this URL into an official Yoti QR - This is important to establish trust between your user base and Yoti. 

{% image url="https://image-archive.developerhub.io/image/upload/29780/wnhb38v4po2wjyilvv7v/1590073166.png" caption="Example QR image" mode="300" height="500" width="500" %}
{% /image %}

{% code %}
{% tab language="markup" %}
POST https://api.yoti.com/api/v1/qrcodes/image
{% /tab %}
{% /code %}

The following headers are required to use the image service:

{% table %}
| Header | Value | Description | 
| ---- | ---- | ---- | 
| Accept | The follow Accept values can be provided in the header\n\n\n\n- image/svg+xml\n- image/png | Returns a formatted QR code as an svg or png | 
{% /table %}

The request body should be formed as JSON, specifying a URL (mandatory) and an image size (option)

{% code %}
{% tab language="json" %}
{
	"url": "https://code.yoti.com/<YotiCode>"
}
{% /tab %}
{% /code %}

{% table %}
| Field | Value | 
| ---- | ---- | 
| url | This is the URL returned from requesting a Yoti QR | 
{% /table %}

**Error codes**

{% table %}
| Code | Description | Resolution | 
| ---- | ---- | ---- | 
| 400 | Missing url field in the request body | Ensure to POST a JSON body containing a url | 
| 406 | Empty Accept header | Send a request Accept header with the required image return type | 
| 406 | An Accept header was sent with an invalid return type | Ensure the Accept header is one of\n\n\n\n- image/svg+xml\n- image/png | 
{% /table %}

**Decoding and resolving the QR code metadata**

In order to decode and resolve the URL returned by the `requesting a QR code`endpoint and retrieve the QR code metadata, it is necessary to:

1. Split the URL by `https://code.yoti.com/` keeping the QR code data, i.e. `CAEaJDlhMzg5MTRiLTg0ZDAtNGI3Zi05NDNiLWQzNzBmNmM3YTVlYzAA`
2. Base 64 url decode the obtained string.

{% code %}
{% tab language="java" %}
byte[] bytes = Base64.getUrlDecoder().decode(str);
{% /tab %}
{% /code %}

Unmarshal the protocol buffer data structure using the following proto definition:

{% code %}
{% tab language="java" %}
syntax = "proto2";
package qrpubapi_v1;
option java_package = "com.yoti.qrpubapi_v1";
option java_outer_classname = "QrCodeMsgProto";
enum Issuer {
    CONNECT = 1;
}
enum Transport {
    UNDEFINED = 0;
    URI = 1;
    QR_CODE = 2;
}
message QrCodeMsg{
    optional Issuer issuer = 1;
    optional bytes sharing_token = 2;
    optional bytes ref_id = 3;
    optional bytes  policy = 4;
    optional Transport transport = 6;
}
{% /tab %}
{% /code %}

{% html %}
<div class="alert-GTK">
    <div class="alert-title" id="GTK">
        Good to know
    </div>
    <div class="alert-text">
Major languages provide protobuf compilers to generate code that automatically handles protocol buffers marshalling/unmarshalling.

If you are using the java protobuf compiler and you have generated your proto stubs, un marshalling the described protocol buffer is very simple.    </div>
    <div class="alert-links"> 
      
    </div>
</div>
{% /html %}

{% code %}
{% tab language="java" %}
QrCodeMsg qrCodeMsg = QrCodeMsg.parseFrom(bytes);
{% /tab %}
{% /code %}

Although there are few fields in the described data structure, we are only interested in the field named "ref_id", since the others are used by the Yoti app, in order to properly handle the scanned code.

The ref_id field must be interpreted as a UTF-8 string (default encoding for the Java language when creating a String object) and used to retrieve the QR code meta data. This can be achieved by invoking the _retrieve QR code metadata_ endpoint:

{% code %}
{% tab language="markup" %}
https://api.yoti.com/api/v1.1/qrcodes/refs/<ref_id>
{% /tab %}
{% /code %}

{% table %}
| Parameter | Description | 
| ---- | ---- | 
| ref_id | This is the UTF-8 string representation of the ref_id field obtained from the proto buffer data structure. | 
{% /table %}

The result of this invocation is a JSON payload that looks like the following:

{% code %}
{% tab language="json" %}
{

  "name": "App name",
  "policy": "CggKBnNlbGZpZQoOCgxwaG9uZV9udW1iZXISEgoQYXBwbGljYXRpb25fbG9nbxIRCg9hcHBsaWNhdGlvbl91cmwSEgoQYXBwbGljYXRpb25fbmFtZRIdChthcHBsaWNhdGlvbl9yZWNlaXB0X2JnY29sb3IYASAA",
  "application_id": "a9c4a5ad-d9e5-4fc8-a561-6eedbc882691",
  "application_name": "Yoti App",
  "receipt_bg_color": "#2D9FFF",
  "callback_endpoint": "https://yoti.com/app",
  "sharing_token": "2z94Ix7B7t6B+C3aUSy/6bBuMzQJYZqEBbQa9fp3O6r0bqRgpp0VveojLu8FxdLT",
  "session_data": "0LBGRyLy-422ef9b5-871f-4fba-8bed-e70bc4a1e650"
}
{% /tab %}
{% /code %}

The field we are interested in is the one named "session_data" and it will be used to establish a web socket channel through which our client will get notified about a successful/failed interaction.

Attribute "callback_endpoint" will be used in the last step of this guide.

**Opening a web socket channel**

Opening a web socket channel to Yoti using the resolved metadata

To create a web socket channel to Yoti servers, it is necessary to hit the following `web socket channel`endpoint using a web socket client:

{% code %}
{% tab language="markup" %}
wss://api.yoti.com/api/v1.1/connect-sessions/<session_data>
{% /tab %}
{% /code %}

{% table %}
| Parameter | Description | 
| ---- | ---- | 
| session_data | The session_data obtained from the call to _retrieve QR code_ endpoint | 
{% /table %}

{% html %}
<div class="alert-GTK">
    <div class="alert-title" id="GTK">
        Good to know
    </div>
    <div class="alert-text">
It is important to know that different clients connect using different schemes: some use the WSS protocol, while others make an https request and expect the server to do the upgrade to WSS (this is the standard approach).  </div>
    <div class="alert-links"> 
      
    </div>
</div>
{% /html %}

Once the connection is established, you will need to send an initial subscription message, the value of this is the session_data used to create the channel. An example of this is shown below.

{% code %}
{% tab language="json" %}
{
	"subscription": <session_data>
}
{% /tab %}
{% /code %}

{% code %}
{% tab language="javascript" %}
var socket = new WebSocket(socketAddress + '/connect-sessions/' + session_data)
socket.onopen = function() {
  socket.send(JSON.stringify({subscription: session_data}))
}
{% /tab %}
{% /code %}

The server will send the following message back over the channel:

{% code %}
{% tab language="json" %}
//successful message
{
  "status" : "ACCEPTED",
  "subscription" : "0LBGRyLy-422ef9b5-871f-4fba-8bed-e70bc4a1e650"
}

// invalid session_data value has been provided,
{
  "status" : "REJECTED",
  "subscription" : "0LBGRyLy-422ef9b5-871f-4fba-8bed-e70bc4a1e650"
}
{% /tab %}
{% /code %}

**Receiving a token**

Receiving a Yoti token over the web socket channel or handling a session error. Assuming the connection was successfully established, a further message will be prompted that signals the completion of the transaction.

If the transaction fails, the server will send the following message:

{% code %}
{% tab language="json" %}
{
  "status" : "FAILED",
  "subscription" : "0LBGRyLy-422ef9b5-871f-4fba-8bed-e70bc4a1e650"
}
{% /tab %}
{% /code %}

If the transaction times out, the server will send the following message:

{% code %}
{% tab language="json" %}
{
  "status" : "TIMED_OUT",
  "subscription" : "0LBGRyLy-422ef9b5-871f-4fba-8bed-e70bc4a1e650"
}
{% /tab %}
{% /code %}

If any of the last two messages occur, you should restart the process by requesting a new QR code.

Let's finally see what happens when a transaction is successfully completed. In this case the server will send the following message:

{% code %}
{% tab language="json" %}
{
  "status" : "COMPLETED",
  "subscription" : "0LBGRyLy-422ef9b5-871f-4fba-8bed-e70bc4a1e650",
  "token" : "egouerghwl4itjxpri4oty5ihfli4yg7tgbnkrliu"
}
{% /tab %}
{% /code %}

The token here is the Yoti token that must be passed to your application back-end, in order to retrieve the user shared profile using the Yoti SDKs.

Below is a javascript example that shows how to implement the logic that is necessary to correctly handle the channel communication.

{% code %}
{% tab language="javascript" %}
var socket = new WebSocket(socketAddress + '/connect-sessions/' + connection)
socket.onopen = function() {
  socket.send(JSON.stringify({subscription: connection}))
}
socket.onmessage = function(e) {
  var message = JSON.parse(e.data)
  switch(message.status) {
    case 'COMPLETED':
      var token = message.token
      // send token to backend here
      break;
    case 'ACCEPTED':                   
      break;
    case 'TIMED_OUT':
      // restart process
      break;
    case 'REJECTED':
      // restart process
      break;
  }
}
{% /tab %}
{% /code %}

**Passing the token to the callback URL**

Passing the received token to the callback url that has been specified in Yoti Hub.

Finally, the received token must be forwarded to your back-end, which should be listening for GET requests at the address specified by the attribute named "callback_endpoint" that has been returned as a response to the request to `requesting a QR code`endpoint. 

The token should be provided as a query string parameter, so, in this example, the client should send a GET request to the follow URL:

{% code %}
{% tab language="markup" %}
https://yoti.com/app?token=egouerghwl4itjxpri4oty5ihfli4yg7tgbnkrliu
{% /tab %}
{% /code %}

It is worth noticing that, in case you are deploying your client in different physical locations, this would be the best point to provide some metadata by personalising your request to your own back-end.

The example above could be extended by providing more parameters:

{% code %}
{% tab language="markup" %}
https://yoti.com/app?token=egouerghwl4itjxpri4oty5ihfli4yg7tgbnkrliu&lane=2&location=WC2N4JH
{% /tab %}
{% /code %}

From here on, it is only a matter of using the Yoti SDK for your favourite language as described in [Web Integration](https://developers.yoti.com/yoti/web-integration).

Your endpoint can return any value in any format, since your client will handle it. Our suggestion is at least to capture the result of the interaction with the Yoti SDK and tell the client whether the interaction succeeded or not.

---

### Dynamic QR

This QR code is generated differently. By "dynamic" we mean that the attributes must be provided as part of the QR code request as opposed to where the attributes is defined upfront in [hub](https://hub.yoti.com/). This allows for higher flexibility, for example as part of your integration you can create a set of fields that must be filled in by the user, the set of required attributes is intrinsically dynamic from Yoti as it depends on the type of information received manually.

Please launch this demo to view how this works: [https://yoti.world/dynamicqr/](https://yoti.world/dynamicqr/).

This section below describes the process of creating a dynamic QR code broken down into the following steps:

1. Creating the policy
2. Creating the scenario
3. Creating a share URL

{% html %}
<div class="alert-BYS">
   <div class="alert-title" id="BYS">
      Before you start
   </div>
   <div class="alert-text" >
      Please install our Yoti SDK.
   </div>
   <div class="alert-links"> 
      <a href="https://developers.yoti.com/yoti/web-integration#install-sdk">Install the SDK</a>
   </div>
</div>
{% /html %}

Full examples are located here:

- [Java](https://github.com/getyoti/yoti-java-sdk/blob/master/yoti-sdk-spring-boot-example/src/main/java/com/yoti/api/examples/springboot/YotiLoginController.java)
- [Node](https://github.com/getyoti/yoti-node-sdk/blob/master/examples/profile/index.js)
- [Ruby](https://github.com/getyoti/yoti-ruby-sdk/blob/master/examples/rails/app/controllers/yoti_controller.rb)
- [Go](https://github.com/getyoti/yoti-go-sdk/blob/master/_examples/profile/main.go)
- [PHP](https://github.com/getyoti/yoti-php-sdk/blob/master/examples/profile/app/Http/Controllers/DynamicShareController.php)
- [Python](https://github.com/getyoti/yoti-python-sdk/blob/master/examples/yoti_example_flask/app.py)
- .[NET](https://github.com/getyoti/yoti-dotnet-sdk/blob/master/src/Examples/Profile/CoreExample/Controllers/HomeController.cs)

**Creating the policy**

A policy is used to define what attributes are requested from the user. You can use the builder to define what attributes are needed. There are multiple different ways to add an attribute to a policy:

1) Using our self built method allowing you to customise the attribute with source constraints.

2) Using our out of the box attribute with default settings, which is no constraints.

3) Easier readable methods with default settings, which is no constraints.

{% code %}
{% tab language="javascript" %}
const selfBuiltAttribute = new Yoti.WantedAttributeBuilder()
    .withName("full_name")
    .withConstraints(constraints)
    .withAcceptSelfAsserted()
    .build();

  const dynamicPolicy = new Yoti.DynamicPolicyBuilder()
  //using an attribute you build
    .withWantedAttribute(selfBuiltAttribute)
  //using an attribute by name
    .withWantedAttributeByName("full_name")
  //using a predefined method to add an attribute
    .withFullName()
  //if you wish the user to prove it's them by taking a selfie on share
    .withSelfieAuthentication()
    .build();
{% /tab %}
{% tab language="java" %}
WantedAttribute selfBuiltAttribute = new SimpleWantedAttributeBuilder()
               .withName("full_name")
               .withAcceptSelfAsserted()
               .build();


       DynamicPolicy dynamicPolicy = new SimpleDynamicPolicyBuilder()
              //using an attribute you build
               .withWantedAttribute(givenNamesWantedAttribute)
              //using an attribute by name
               .withWantedAttribute(true,"full_name")
               //using a predefined method to add an attribute
               .withFullName()
               //if you wish the user to prove it's them by taking a selfie on share
               .withSelfieAuthorisation(true)
               .build();
{% /tab %}
{% tab language="php" %}
<?php

use Yoti\ShareUrl\Policy\WantedAttributeBuilder;
use Yoti\ShareUrl\Policy\DynamicPolicyBuilder;

$selfBuiltAttribute = (new WantedAttributeBuilder())
    ->withName("full_name")
    ->withConstraints(constraints)
    ->withAcceptSelfAsserted()
    ->build();

$dynamicPolicy = (new DynamicPolicyBuilder())
   //using an attribute you build
   ->withWantedAttribute(selfBuiltAttribute)
   //using an attribute by name
   ->withWantedAttributeByName("full_name")
   //using a predefined method to add an attribute
   ->withFullName()
   //if you wish the user to prove it's them by taking a selfie on share
   ->withSelfieAuthentication()
   ->build();
{% /tab %}
{% tab language="python" %}
from yoti_python_sdk.dynamic_sharing_service.policy import (
    DynamicPolicyBuilder,
    WantedAttributeBuilder,
)

selfBuiltAttribute = (WantedAttributeBuilder()
                      .with_name("full_name")
                      .with_constraint(constraints)
                      .with_accept_self_asserted()
                      .build()
                      )

dynamicPolicy = (DynamicPolicyBuilder()
                 #   using an attribute you build
                 .with_wanted_attribute(selfBuiltAttribute)
                 #   using an attribute by name
                 .with_wanted_attribute("full_name")
                 #   using a predefined method to add an attribute
                 .with_full_name()
                 #   if you wish the user to prove it's them by taking a selfie on share
                 .with_selfie_auth()
                 .build()
                 )
{% /tab %}
{% tab language="go" %}
package main

import (
	"github.com/getyoti/yoti-go-sdk/v3"
	"github.com/getyoti/yoti-go-sdk/v3/dynamic"
)


selfBuiltAttribute := (
	&dynamic.PolicyBuilder{})
	.WithName("full_name")
    .WithConstraints(constraints)
    .WithAcceptSelfAsserted()
    .Build();
)

dynamicPolicy := (
	&dynamic.WantedAttributeBuilder{})
	//using an attribute you build
	.WithWantedAttribute(selfBuiltAttribute)
	//using an attribute by name
	.withWantedAttributeByName("full_name")
	//using a predefined method to add an attribute
	.WithFullName()
	//if you wish the user to prove it's them by taking a selfie on share
	.WithSelfieAuth()
	.Build()
)
{% /tab %}
{% tab language="csharp" %}
var selfBuiltAttribute = new Yoti.WantedAttributeBuilder()
  .withName("full_name")
  .withConstraints(constraints)
  .withAcceptSelfAsserted()
  .build();

var dynamicPolicy = new Yoti.DynamicPolicyBuilder()
  //using an attribute you build
  .withWantedAttribute(selfBuiltAttribute)
  //using an attribute by name
  .withWantedAttributeByName("full_name")
  //using a predefined method to add an attribute
  .withFullName()
  //if you wish the user to prove it's them by taking a selfie on share
  .withSelfieAuthentication()
  .build();
{% /tab %}
{% /code %}

You can apply [constraints](https://developers.yoti.com/yoti/knowledge-base-hub#source-and-verifiers) to an attribute. The only available constraint is to limit the source of the attribute, eg. to limit full_name to only come from a passport. 

If a constraint has "soft preference" set to 'true' then the attribute will still be shared from another source if it the specified source is not present.

{% code %}
{% tab language="javascript" %}
const sourceConstraint = new Yoti.SourceConstraintBuilder()
   //passport
    .withPassport()
   //Driving Licence
    .withDrivingLicence()
   //National ID
    .withNationalId()
   //Passcard
    .withPasscard()
 
    .withSoftPreference(false)
    .build();

  const constraints = new Yoti.ConstraintsBuilder()
    .withSourceConstraint(sourceConstraint)
    .build();

const selfBuiltAttribute = new Yoti.WantedAttributeBuilder()
    .withName("full_name")
    .withConstraints(constraints)
    .withAcceptSelfAsserted()
    .build();
{% /tab %}
{% tab language="java" %}
WantedAnchor passportAnchor = new SimpleWantedAnchorBuilder()
                .withValue("PASSPORT")
                .build();

        WantedAnchor drivingLicenceAnchor = new SimpleWantedAnchorBuilder()
                .withValue("DRIVING_LICENCE")
                .build();

        WantedAnchor nationalIdAnchor = new SimpleWantedAnchorBuilder()
                .withValue("NATIONAL_ID")
                .build();

        WantedAnchor passcardAnchor = new SimpleWantedAnchorBuilder()
                .withValue("PASSCARD")
                .build();

        SourceConstraint sourceConstraint = new SimpleSourceConstraintBuilder()
                //Passport
                .withWantedAnchor(passportAnchor)
                //Driving Licence
                .withWantedAnchor(drivingLicenceAnchor)
                //National ID
                .withWantedAnchor(nationalIdAnchor)
                //Passcard
                .withWantedAnchor(passcardAnchor)
                .withSoftPreference(false)
                .build();


        WantedAttribute selfBuiltAttribute = new SimpleWantedAttributeBuilder()
                .withName("full_name")
                .withConstraint(sourceConstraint)
                .withAcceptSelfAsserted(true)
                .build();
{% /tab %}
{% tab language="go" %}
package main

import (
	"github.com/getyoti/yoti-go-sdk/v3"
	"github.com/getyoti/yoti-go-sdk/v3/dynamic"
)

sourceConstraint := (
	&dynamic.SourceConstraintBuilder()
	//passport
	 .WithPassport()
	//Driving Licence
	 .WithDrivingLicence()
	//National ID
	 .WithNationalId()
	//Passcard
	 .WithPasscard()
  
	 .WithSoftPreference(false)
	 .Build();
)

constraints := (
	&dynamic.ConstraintsBuilder()
	 .WithSourceConstraint(sourceConstraint)
	 .Build();
)
 
selfBuiltAttribute := (
	&dynamic.WantedAttributeBuilder()
	 .WithName("full_name")
	 .WithConstraints(constraints)
	 .WithAcceptSelfAsserted()
	 .Build();
)
{% /tab %}
{% tab language="python" %}
from yoti_python_sdk.dynamic_sharing_service.policy import (
    SourceConstraintBuilder,
    ConstraintsBuilder
    WantedAttributeBuilder,
)
                 
sourceConstraint = (SourceConstraintBuilder()
   #passport
    .with_passport()
   #Driving Licence
    .with_driving_licence()
   #National ID
    .with_national_id()
   #Passcard
    .with_passcard()
 
    .with_soft_preference(false)
    .build()
)

constraints = (ConstraintsBuilder()
    .with_source_sonstraint(sourceConstraint)
    .build()
  )

selfBuiltAttribute = (WantedAttributeBuilder()
    .with_name("full_name")
    .with_constraints(constraints)
    .with_accept_self_asserted()
    .build()
    )
{% /tab %}
{% tab language="php" %}
<?php

use Yoti\ShareUrl\Policy\WantedAttributeBuilder;
use Yoti\ShareUrl\Policy\ConstraintsBuilder;
use Yoti\ShareUrl\Policy\SourceConstraintBuilder;


$sourceConstraint = (new SourceConstraintBuilder())
  //passport
  ->withPassport()
  //Driving Licence
  ->withDrivingLicence()
  //National ID
  ->withNationalId()
  //Passcard
  ->withPasscard()

  ->withSoftPreference(false)
  ->build();

$constraints = (new ConstraintsBuilder())
->withSourceConstraint(sourceConstraint)
  ->build();

$selfBuiltAttribute = (new WantedAttributeBuilder())
->withName("full_name")
  ->withConstraints(constraints)
  ->withAcceptSelfAsserted()
  ->build();
{% /tab %}
{% tab language="csharp" %}
var sourceConstraint = new Yoti.SourceConstraintBuilder()
  //passport
  .withPassport()
  //Driving Licence
  .withDrivingLicence()
  //National ID
  .withNationalId()
  //Passcard
  .withPasscard()

  .withSoftPreference(false)
  .build();

var constraints = new Yoti.ConstraintsBuilder()
  .withSourceConstraint(sourceConstraint)
  .build();

var selfBuiltAttribute = new Yoti.WantedAttributeBuilder()
  .withName("full_name")
  .withConstraints(constraints)
  .withAcceptSelfAsserted()
  .build();
{% /tab %}
{% /code %}

{% html %}
<div class="alert-GTK">
    <div class="alert-title" id="GTK">
        Good to know
    </div>
    <div class="alert-text">
For information on our supported attributes and sources please head over to the below sections.    </div>
    <div class="alert-links"> 
       <a href="https://developers.yoti.com/yoti/knowledge-base-hub#yoti-attributes-explained">Yoti Attributes explained</a>
      <a href="https://developers.yoti.com/yoti/knowledge-base-hub#source-and-verifiers">Source and verifiers<a>
    </div>
</div>
{% /html %}

**Creating a scenario**

The Dynamic Scenario is built using:

- The policy
- A callback URL for share completion. After the share is completed, the callback URL is where the user will be redirected to the specified page. A one time use token will be added to the URL. You can use this token to[ retrieve the profile](https://developers.yoti.com/yoti/web-integration#retrieve-a-profile) of the share.
- Any extensions - see below section: Extra features.

{% code %}
{% tab language="javascript" %}
const dynamicScenario = new Yoti.DynamicScenarioBuilder()
      .withCallbackEndpoint("/your-callback")
      .withPolicy(dynamicPolicy)
      //if using an extension
      .withExtension(extension)
  
      .build();
{% /tab %}
{% tab language="java" %}
DynamicScenario dynamicScenario = new SimpleDynamicScenarioBuilder()
                .withCallbackEndpoint("/your-callback")
                .withPolicy(dynamicPolicy)
                //if using an extension
                .withExtension(extension)
                .build();
{% /tab %}
{% tab language="python" %}
from yoti_python_sdk.dynamic_sharing_service.policy import (
		DynamicScenarioBuilder
)

dynamicScenario = (DynamicScenarioBuilder()
                   .with_callback_endpoint("/your-callback")
                   .with_policy(dynamicPolicy)
                   # if using an extension
                   .with_extension(extension)

                   .build()
                   )
{% /tab %}
{% tab language="csharp" %}
var dynamicScenario = new Yoti.DynamicScenarioBuilder()
  .withCallbackEndpoint("/your-callback")
  .withPolicy(dynamicPolicy)
  //if using an extension
  .withExtension(extension)

  .build();
{% /tab %}
{% tab language="go" %}
dynamicScenario = := (
	&dynamic.DynamicScenarioBuilder()
  		.WithCallbackEndpoint("/your-callback")
  		.WithPolicy(dynamicPolicy)
  		//if using an extension
  		.WithExtension(extension)

		  .Build();
)
{% /tab %}
{% tab language="php" %}
<?php

use Yoti\ShareUrl\Policy\DynamicScenarioBuilder;

$dynamicScenario = (new DynamicScenarioBuilder())
  ->withCallbackEndpoint("/your-callback")
  ->withPolicy(dynamicPolicy)
  //if using an extension
  ->withExtension(extension)

  ->build();
{% /tab %}
{% /code %}

**Create a share URL**

Using the dynamic scenario you need to get a shareURL which will be used by the Yoti scripts to generate a Yoti QR code.

{% table %}
| Example | 
| ---- | 
| [https://code.yoti.com/CAEaJDI5ZjEyZmI4LTMyNTYtNDI0NS05OTg3LTBkMTA0ZTQ2N2JkYjAC](https://code.yoti.com/CAEaJDI5ZjEyZmI4LTMyNTYtNDI0NS05OTg3LTBkMTA0ZTQ2N2JkYjAC) | 
{% /table %}

{% code %}
{% tab language="javascript" %}
yotiClient.createShareUrl(dynamicScenario)
    .then((shareUrlResult) => {
     const shareURL =  shareUrlResult.getShareUrl(),
    }).catch((error) => {
      console.error(error.message);
    });
{% /tab %}
{% tab language="java" %}
try {
        String shareUrl = client.createShareUrl(dynamicScenario).getUrl();
        } catch (DynamicShareException e) {
            LOG.error(e.getMessage());
        }
{% /tab %}
{% /code %}

Once you have your share URL you can send it to the frontend for it to be rendered in a Yoti QR code. Please see example below using the modal QR code.

{% code %}
{% tab language="html" %}
<!-- Simple Button Generation -->

<head>
  <script src="https://www.yoti.com/share/client/"></script>
</head>

<body>
  <!-- Yoti element will be rendered inside this DOM node -->
  <div id="xxx"></div>

  <!-- This script snippet will also be required in your HTML body -->
  <script>
    window.Yoti.Share.init({
      elements: [
        {
          domId: "xxx",
          shareUrl: "shareURL",
          clientSdkId: "xxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx",
          displayLearnMoreLink: true,
        }
      ]
    });
  </script>
</body>
{% /tab %}
{% /code %}

{% html %}
<div class="alert-GTK">
    <div class="alert-title" id="GTK">
        Good to know
    </div>
    <div class="alert-text">
        To generate your dynamic QR code on your front end you will need the shareURL and SDK ID from your application.
    </div>
    <div class="alert-links"> 
        <a target="_self" href="https://developers.yoti.com/yoti/web-integration#modal">See here for all the QR types</a>
   </div>
</div>
{% /html %}

### Location constraint

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
| Latitude | Decimal Degrees | Device's latitude | 
| Longitude | Decimal Degrees | Device's longitude | 
| Radius | Meters | Radius of the circle centred on the specified location coordinates where the device is allowed to perform the share. (Default 150) | 
| Max Uncertainty | Meters | Maximum acceptable length of the radius representing the area of uncertainty associated with the device location coordinates. (Default 150) | 
{% /table %}

{% code %}
{% tab language="javascript" %}
const dynamicScenario = new Yoti.DynamicScenarioBuilder()
      .withCallbackEndpoint("/your-callback")
      .withPolicy(dynamicPolicy)
      //if using an extension
      .withExtension(Locationextension)
      .build();
{% /tab %}
{% /code %}

---

### Verifiable credential

A verifiable credential​ is handled in the same way as any Yoti [attribute](https://developers.yoti.com/yoti/knowledge-base-hub#general-attributes) but follows the same concept as the [W3C standard](https://www.w3.org/TR/vc-data-model/#what-is-a-verifiable-credential). The definition of an attribute is an assertion made about a user. It can be identity information, something that the user owns and can prove they are in control of. 

A verifiable credential allows you to issue your own 'attribute' to a Yoti user. This document will walk you through our API giving the ability to choose who is able to both issue and request these credentials in the
credential definition stage.

{% image url="https://image-archive.developerhub.io/image/upload/29780/y4hai4rjsnzw27bhdodt/1601481846.png" caption="Credential creation with Yoti" mode="responsive" height="342" width="1272" %}
{% /image %}

{% html %}
<div class="alert-GTK">
    <div class="alert-title" id="GTK">
        Good to know
    </div>
    <div class="alert-text">
        If you wish to use this functionality please let us know as this process currently requires us to do a Yoti app change internally.
    </div>
    <div class="alert-links"> 
        <a href="mailto:sdksupport@yoti.com">SDK Support contact</a>
   </div>
</div>
{% /html %}

There are three main stages to create and use your credential:

- Defining the credential.
- Issuing the credential.
- Requesting the credential.

{% html %}
<div class="alert-BYS">
   <div class="alert-title" id="BYS">
      Before you start
   </div>
   <div class="alert-text" >
      Please install our Yoti SDK and get familiar with our dynamic QR code.
   </div>
   <div class="alert-links"> 
      <a href="https://developers.yoti.com/yoti/web-integration#install-sdk">Install the SDK</a>
           <a href="https://developers.yoti.com/yoti/advanced-features#dynamic-qr">Dynamic QR code</a>
   </div>
</div>
{% /html %}

**Defining the credential**

At the definition stage you will define:

- The name of the credential
- The format and structure of the credential - Yoti currently supports, Text (single line), JPEG, PNG and JSON object.
- Who can issue it
- Who can retrieve it

You will need to create the definition, using the Yoti SDK. This is a one-time process which will be used and referenced for every credential issuance. 

Once you have added the Yoti SDK dependency to your project, you can use it to build and send your request. See the code snippets below for examples of how to construct the request.

{% code %}
{% tab language="javascript" %}
COMING SOON
{% /tab %}
{% tab language="ruby" %}
COMING SOON
{% /tab %}
{% tab language="csharp" %}
string json = JsonConvert.SerializeObject(deserializedObject);
byte[] httpContent = System.Text.Encoding.UTF8.GetBytes(jsonString);

var signedRequest = new RequestBuilder()
	.WithBaseUri(new Uri("https://api.yoti.com/api/v1/attribute-registry"))
	.WithEndpoint("/definitions")
	.WithHttpMethod(HttpMethod.Post)
	.WithHeader("X-Yoti-Auth-Id", _clientSdkId)
	.WithKeyPair(keyPair)
	.WithContent(httpContent)
	.Build();
{% /tab %}
{% tab language="python" %}
COMING SOON
{% /tab %}
{% tab language="java" %}
COMING SOON
{% /tab %}
{% tab language="go" %}
COMING SOON
{% /tab %}
{% tab language="php" %}
string json = JsonConvert.SerializeObject(deserializedObject);
byte[] httpContent = System.Text.Encoding.UTF8.GetBytes(jsonString);

var signedRequest = new RequestBuilder()
	.WithBaseUri(new Uri("https://api.yoti.com/api/v1/attribute-registry"))
	.WithEndpoint("/definitions")
	.WithHttpMethod(HttpMethod.Post)
	.WithHeader("X-Yoti-Auth-Id", _clientSdkId)
	.WithKeyPair(keyPair)
	.WithContent(httpContent)
	.Build();
{% /tab %}
{% /code %}

{% table %}
| Parameter | Description | 
| ---- | ---- | 
| sdkId | sdkId is the SDK_ID found with your Yoti Hub Application | 
| keyPair | The PEM file which is found with your Yoti Hub Application. The PEM file is required to allow the SDK to perform the authentication with the Yoti API. | 
{% /table %}

**Example payload**

{% code %}
{% tab language="json" %}
{
  "name": "credential name",
  "mimeType": "application/json",
  "config": {
    "accessProperties": {
      "requestors": [],
      "publiclyAccessible": true
    },
    "localisationProperties": {
      "defaultLocalisation": {
        "locale": "en_GB",
        "value": "Example.com identifier"
      }
    },
    "issuanceProperties": {
      "maxCardinality": 1,
      "issuers": [
        {
          "domain": "example.com"
        }
      ],
      "issuanceURL": "https://www.example.com/get-identifier"
    },
    "displayProperties": {
      "displayValueMimeType": "text/plain",
    }
  }
}
{% /tab %}
{% /code %}

See below for explanation of example payload:

{% table %}
| Parameter | Description | Optional | 
| ---- | ---- | ---- | 
| Name | This is the name of the credential. This is what will appear on the users Yoti app. | N | 
| MimeType | This will declare what type of credential you want. We currently support:\n\ntext/plain, application/JSON, image/png, image/jpeg. | N | 
| Access properties | This is where you define who will be allowed to request the credential. \n\n\n\nThis should be in a fully qualified domain name format.\n\n\n\nIf publicly accessibility is 'True' then the credential can be requested publicly in their Yoti share. If you would like to control which organisations will request this credential please state 'False' here. | N | 
| Localisations properties | This is used to translate the name of the credential as it appears on the Yoti app. This should be in a fully qualified domain name format. \n\nNote: This functionality is not active yet. | Y | 
| Issuance properties | This is where you define who will be allowed to issue the credential. \n\nThis should be in a fully qualified domain name format. | N | 
| Issuance URL | Here you can provide a URL for information on how to obtain the credential. | Y | 
| displayProperties | Customisation of the credential will be configured here. \n\nNote: This functionality is not active yet. | Y | 
{% /table %}

By supplying the credential in the format of a JSON object, this will allow you to bundle multiple pieces of information together in a single credential request. As an example, you could ask for the credential Employee Number. If this is supplied via a JSON object, within that credential can also contain various other bits of information such as name, email address, access level etc.

**Example response**

{% code %}
{% tab language="json" %}
{
  "id": "uuid"
}
{% /tab %}
{% /code %}

**Issuing an credential**

{% html %}
<div class="alert-BYS">
   <div class="alert-title" id="BYS">
      Before you start
   </div>
   <div class="alert-text" >
      Please get familiar with our dynamic QR code.
   </div>
   <div class="alert-links"> 
           <a href="https://developers.yoti.com/yoti/advanced-features#dynamic-qr">Dynamic QR code</a>
   </div>
</div>
{% /html %}

To issue a credential use the dynamic QR code functionality and the third party attribute extension:

{% code %}
{% tab language="javascript" %}
const expiryDate = new Date();
expiryDate.setDate(expiryDate.getDate() + 1);

const thirdPartyAttributeExtension = new ThirdPartyAttributeExtensionBuilder()
    .withDefinition('com.example.someAttribute')
    .withExpiryDate(expiryDate)
    .build();

const dynamicPolicy = (new DynamicPolicyBuilder())
    .withWantedRememberMe(true)
    .build();

const dynamicScenario = (new DynamicScenarioBuilder())
    .withCallbackEndpoint('/issue-attribute')
    .withPolicy(dynamicPolicy)
    .withExtension(thirdPartyAttributeExtension)
    .build();

const shareUrlResult = yotiClient.createShareUrl(dynamicScenario);
{% /tab %}
{% tab language="ruby" %}
seconds_in_day = 86_400
expiry_date = Time.new + seconds_in_day

extension = Yoti::DynamicSharingService::ThirdPartyAttributeExtension
            .builder
            .with_expiry_date(expiry_date)
            .with_definitions('com.example.someAttribute')
            .build

policy = Yoti::DynamicSharingService::DynamicPolicy
         .builder
         .with_wanted_remember_me_id(true)
         .build

scenario = Yoti::DynamicSharingService::DynamicScenario
           .builder
           .with_callback_endpoint('/issue-attribute')
           .with_policy(policy)
           .with_extension(extension)
           .build

share_url_result = Yoti::DynamicSharingService.create_share_url(scenario)
{% /tab %}
{% tab language="csharp" %}
var thirdPartyAttributeExtension = new ThirdPartyAttributeExtensionBuilder()
	.WithDefinition(_thirdPartyAttributeName)
	.WithExpiryDate(DateTime.Today.AddDays(1))
	.Build();

DynamicPolicy dynamicPolicy = new DynamicPolicyBuilder()
	.WithRememberMeId(required: true)
	.Build();

DynamicScenario dynamicScenario = new DynamicScenarioBuilder()
	.WithCallbackEndpoint("/home/issueattribute") //issueAttribute callback
	.WithPolicy(dynamicPolicy)
	.WithExtension(thirdPartyAttributeExtension)
        .Build();

ShareUrlResult shareUrlResult = yotiClient.CreateShareUrl(dynamicScenario);
{% /tab %}
{% tab language="python" %}
from datetime import datetime

from yoti_python_sdk import Client

from yoti_python_sdk.dynamic_sharing_service import (
    create_share_url,
    DynamicScenarioBuilder,
)

from yoti_python_sdk.dynamic_sharing_service.policy.dynamic_policy_builder import (
    DynamicPolicyBuilder,
)

from yoti_python_sdk.dynamic_sharing_service.extension.third_party_attribute_extension import (
    ThirdPartyAttributeExtension,
)

client = Client("YOTI_CLIENT_SDK_ID", "/path/to/key.pem")

expiry_date = datetime.datetime.now() + datetime.timedelta(days=1)

extension = (
    ThirdPartyAttributeExtension()
    .with_expiry_date(expiry_date)
    .with_definitions("com.example.someAttribute")
    .build()
)

policy = (
    DynamicPolicyBuilder()
    .with_wanted_remember_me()
    .build()
)

scenario = (
    DynamicScenarioBuilder()
    .with_callback_endpoint("/issue-attribute")
    .with_policy(policy)
    .with_extension(extension)
    .build()
)

share_url_result = share = create_share_url(client, scenario)
{% /tab %}
{% tab language="java" %}
Date date = new Date();
Calendar calendar = Calendar.getInstance();
calendar.setTime(date);
calendar.add(Calendar.HOUR_OF_DAY, 5);
 
Date expiryDate = calendar.getTime();
 
ThirdPartyAttributeExtensionBuilder thirdPartyAttributeExtensionBuilder = ExtensionBuilderFactory.newInstance()
    .createThirdPartyAttributeExtensionBuilder();
 
Extension<ThirdPartyAttributeContent> thirdPartyAttributeExtension = thirdPartyAttributeExtensionBuilder
    .withExpiryDate(expiryDate)
    .withDefinition("com.example.someAttribute")
    .build();
 
DynamicPolicy dynamicPolicy = new SimpleDynamicPolicyBuilder()
    .withWantedRememberMe(true)
    .build();
 
DynamicScenario dynamicScenario = new SimpleDynamicScenarioBuilder()
    .withCallbackEndpoint("/issue")
    .withPolicy(dynamicPolicy)
    .withExtension(thirdPartyAttributeExtension)
    .build();
{% /tab %}
{% tab language="go" %}
expiryDate := time.Now().AddDate(0, 0, 1)

thirdPartyExtension, err := (&extension.ThirdPartyAttributeExtensionBuilder{}).
	WithExpiryDate(&expiryDate).
	WithDefinition(attribute.NewAttributeDefinition(thirdPartyAttributeName)).
	Build()
if err != nil {
	panic(err)
}

var policy dynamic.Policy
policy, err = (&dynamic.PolicyBuilder{}).
	WithWantedRememberMe().
	Build()

if err != nil {
	panic(err)
}

var scenario dynamic.Scenario
scenario, err = (&dynamic.ScenarioBuilder{}).
	WithCallbackEndpoint("/issue-attribute").
	WithPolicy(policy).
	WithExtension(thirdPartyExtension).
	Build()
if err != nil {
	panic(err)
}

var share dynamic.ShareURL
share, err = client.CreateShareURL(&scenario)
if err != nil {
	panic(err)
}
{% /tab %}
{% tab language="php" %}
<?php

use Yoti\ShareUrl\DynamicScenarioBuilder;
use Yoti\ShareUrl\Extension\ThirdPartyAttributeExtensionBuilder;
use Yoti\ShareUrl\Policy\DynamicPolicyBuilder;

$thirdPartyAttributeExtension = (new ThirdPartyAttributeExtensionBuilder())
    ->withDefinition('com.example.someAttribute')
    ->withExpiryDate(new \DateTime('+1 day'))
    ->build();

$dynamicPolicy = (new DynamicPolicyBuilder())
    ->withWantedRememberMe(true)
    ->build();

$dynamicScenario = (new DynamicScenarioBuilder())
    ->withCallbackEndpoint('/issue-attribute')
    ->withPolicy($dynamicPolicy)
    ->withExtension($thirdPartyAttributeExtension)
    ->build();

$shareUrlResult = $yotiClient->createShareUrl($dynamicScenario);
{% /tab %}
{% /code %}

{% table %}
| Parameter | Description | 
| ---- | ---- | 
| withDefinition() | This value will be your credential name “com.example.someAttribute” | 
| withExpiryDate() | The expired date indicates by when the credential should be issued by. If the credential is not issued by that time, the issuance request will be automatically cancelled.\n\n\n\nIt conforms to RFC3339 (e.g.: 2006-01-02T22:04:05.123Z) | 
| Dynamic policy | This is where you define all your [attributes](https://developers.yoti.com/yoti/knowledge-base-hub#general-attributes) you wish to retrieve from the user. You may set source constraints to ensure only an individual can only share data from a particular document. The soft preference set to 'false' will ensure this is enforced. Please see [dynamic QR code](https://developers.yoti.com/yoti/advanced-features#dynamic-qr) section for more details on this. | 
| Dynamic scenario | Build the scenario with the third-party extension request and share policy request. | 
{% /table %}

**Get credential issuance details**

The credential issuance details will include an issuance token. 

{% html %}
<div class="alert-GTK">

    <div class="alert-title" id="GTK">

        Note.. 

    </div>

    <div class="alert-text">

This should be stored as part of the customer record as this will be required for issuing the credential and revoking / updating the credential in the future.
    </div>

</div>
{% /html %}

{% code %}
{% tab language="javascript" %}
const activityDetails = await yotiClient.getActivityDetails(token);
const attributeIssuanceDetails = activityDetails.getExtraData().getAttributeIssuanceDetails();
const issuingAttributes = attributeIssuanceDetails.getIssuingAttributes();
{% /tab %}
{% tab language="ruby" %}
activity_details = Yoti::Client.get_activity_details(token)
attribute_issuance_details = activity_details.extra_data.attribute_issuance_details
{% /tab %}
{% tab language="csharp" %}
var httpClient = new HttpClient();

var activityDetails = yotiClient.GetActivityDetails(token);
var attributeIssuanceDetails = activityDetails.ExtraData.AttributeIssuanceDetails;
{% /tab %}
{% tab language="python" %}
activity_details = client.get_activity_details(token)
attribute_issuance_details = activity_details.extra_data.attribute_issuance_details
{% /tab %}
{% tab language="java" %}
activityDetails = client.getActivityDetails(token);

ExtraData extraData = activityDetails.getExtraData();

AttributeIssuanceDetails attributeIssuanceDetails = extraData.getAttributeIssuanceDetails();

String issuanceToken = attributeIssuanceDetails.getToken();
{% /tab %}
{% tab language="go" %}
activityDetails, err := client.GetActivityDetails(token)
if err != nil {
	panic(err)
}

issuingAttributes := activityDetails.ExtraData().AttributeIssuanceDetails()
{% /tab %}
{% tab language="php" %}
<?php

$activityDetails = $yotiClient->getActivityDetails($token);
$attributeIssuanceDetails = $activityDetails->getExtraData()->getAttributeIssuanceDetails();
{% /tab %}
{% /code %}

**Request for credential to be issued**

The credential value is now ready to be issued to the Yoti user which is the schema of the credential. You will need to provide the issuance token, the name and the payload below. 

{% code %}
{% tab language="javascript" %}
const payload = new Payload({
    issuance_token: attributeIssuanceDetails.getToken(),
    attributes: [
        {
            name: 'com.example.someAttribute',
            value: 'some attribute value',
        },
    ],
});

const request = new RequestBuilder()
    .withBaseUrl('https://api.yoti.com/api/v1/attribute-registry')
    .withEndpoint('/attributes')
    .withPemString('PEM_CONTENT')
    .withHeader('X-Yoti-Auth-Id', 'CLIENT_SDK_ID')
    .withMethod('POST')
    .withPayload(payload)
    .build();

const response = await request.execute();

// Note:
// - Use RequestBuilder::withPemFilePath() to provide a file path
//   (This may have performance implications)
{% /tab %}
{% tab language="ruby" %}
payload = {
  issuance_token: attribute_issuance_details.token,
  attributes: [
    {
      name: 'com.example.someAttribute',
      value: 'some attribute value'
    }
  ]
}

request = Yoti::Request
          .builder
          .with_base_url('https://api.yoti.com/api/v1/attribute-registry')
          .with_http_method('POST')
          .with_endpoint('attributes')
          .with_payload(payload)
          .with_header('X-Yoti-Auth-Id', Yoti.configuration.client_sdk_id)
          .build

response = request.execute
{% /tab %}
{% tab language="csharp" %}
var attributeDefinition = new Yoti.Auth.Share.ThirdParty.AttributeDefinition(attributeIssuanceDetails.IssuingAttributes[0].Name);
var attributeValue = "chosenAttributeValue";

string serializedRequest = JsonConvert.SerializeObject(
new {
	issuance_token = attributeIssuanceDetails.Token,
	attributes = new[]
	{
		new {
			name = _thirdPartyAttributeName,
			value = "chosenAttributeValue" // if type==JSON, this needs to be base64-encoded
		}
	}
});

byte[] httpContent = System.Text.Encoding.UTF8.GetBytes(serializedRequest);

var signedRequest = new RequestBuilder()
	.WithBaseUri(new Uri("https://api.yoti.com/api/v1/attribute-registry"))
	.WithEndpoint("/attributes")
	.WithHttpMethod(HttpMethod.Post)
	.WithHeader("X-Yoti-Auth-Id", _clientSdkId)
	.WithKeyPair(keyPair)
	.WithContent(httpContent)
	.Build();

var result = signedRequest.Execute(httpClient).Result;

if (!result.IsSuccessStatusCode)
	throw new InvalidOperationException($"StatusCode: {result.StatusCode}, Content: {result.Content.ReadAsStringAsync().Result}");
{% /tab %}
{% tab language="python" %}
import json

from yoti_python_sdk.http import SignedRequest

payload_data = {
    "issuance_token": attribute_issuance_details.token,
    "attributes": [
        {
            "name": "com.example.someAttribute",
            "value": "some attribute value"
        }
    ]
}

payload_string = json.dumps(payload_data).encode()

signed_request = (
    SignedRequest
    .builder()
    .with_pem_file("/path/to/key.pem")
    .with_base_url("https://api.yoti.com/api/v1/attribute-registry")
    .with_endpoint("/attributes")
    .with_http_method("POST")
    .with_header("X-Yoti-Auth-Id", "CLIENT_SDK_ID")
    .with_payload(payload_string)
    .build()
)

response = signed_request.execute()
{% /tab %}
{% tab language="java" %}
byte[] payload = ...; // Payload is JSON converted to byte array
 
SignedRequest signedRequest = SignedRequestBuilder.newInstance()
            .withKeyPair(YOUR_KEY_PAIR)
            .withBaseUrl("https://api.yoti.com/api/v1/attribute-registry")
            .withEndpoint("/attributes")
            .withHttpMethod("POST")
            .withPayload(payload)
            .build();
 
// 'SomeModel' is a POJO that has been defined by the user and is
// used to map JSON response as the SDK doesn't have any built in
// classes to support this
SomeModel someModel = signedRequest.execute(SomeModel.class);
 
/**
 * SignedRequest.execute() uses built in Java HTTP connectivity.
 * To use another framework if required (e.g. apache), you can get
 * all of the pieces of the Yoti signed request off the SignedRequest
 * object e.g.
**/
URI uri = signedRequest.getUri();
String httpMethod = signedRequest.getMethod();
byte[] payloadData = signedRequest.getData();
Map<String, String> headers = signedRequest.getHeaders();
{% /tab %}
{% tab language="go" %}
type Attribute struct {
	Name  string `json:"name"`
	Value string `json:"value"`
}

type Payload struct {
	Token      string      `json:"token"`
	Attributes []Attribute `json:"attributes"`
}

body, err := json.Marshal(Payload{
	Token: issuingAttributes.Token(),
	Attributes: []Attribute{
		Attribute{
			Name:  "com.example.someAttribute",
			Value: "some attribute value",
		},
	},
})
if err != nil {
	panic(err)
}

headers := map[string][]string{
	"X-Yoti-Auth-Id": []string{"CLIENT_SDK_ID"},
}

decodedKey, err := cryptoutil.ParseRSAKey(key)
if err != nil {
	panic(err)
}

request, err := requests.SignedRequest{
	Key:        decodedKey,
	HTTPMethod: http.MethodPost,
	BaseURL:    "https://api.yoti.com/api/v1/attribute-registry",
	Endpoint:   "/attributes",
	Headers:    headers,
	Body:       body,
}.Request()
if err != nil {
	panic(err)
}

response, err := requests.Execute(&http.Client{}, request)
{% /tab %}
{% tab language="php" %}
<?php

use Yoti\Http\Payload;
use Yoti\Http\RequestBuilder;

$payload = Payload::fromJsonData((object) [
    'issuance_token' => $attributeIssuanceDetails->getToken(),
    'attributes' => [
        (object) [
            'name' => 'com.example.someAttribute',
            'value' => 'some attribute value',
        ],
    ],
]);

$request = (new RequestBuilder())
    ->withBaseUrl('https://api.yoti.com/api/v1/attribute-registry')
    ->withEndpoint('/attributes')
    ->withPemFilePath('/path/to/key.pem')
    ->withHeader('X-Yoti-Auth-Id', 'CLIENT_SDK_ID')
    ->withMethod('POST')
    ->withPayload($payload)
    ->build();

$response = $request->execute();

if ($response->getStatusCode() !== 201) {
    // Handle error.
}

// Note:
// - Use RequestBuilder::withPemFile() to provide a `\Yoti\Util\PemFile`
// - Use RequestBuilder::withPemString() to provide PEM string
{% /tab %}
{% /code %}

The user will now have the credential.

**Requesting the credential**

You will then need to generate a QR code to retrieve the newly-issued credential. The share result will contain the QR code URL to present the [dynamic QR code](https://developers.yoti.com/yoti/advanced-features#dynamic-qr).

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
{% tab language="java" %}
DynamicPolicy dynamicPolicy = new SimpleDynamicPolicyBuilder()
    .withWantedAttribute(false, "com.example.someAttribute")
    .build();
 
DynamicScenario dynamicScenario = new SimpleDynamicScenarioBuilder()
    .withCallbackEndpoint("/account/connect")
    .withPolicy(dynamicPolicy)
    .build();
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

$shareUrlResult = $yotiClient->createShareUrl($dynamicScenario);
{% /tab %}
{% /code %}

{% html %}
<div class="alert-GTK">
    <div class="alert-title" id="GTK">
        Good to know
    </div>
    <div class="alert-text">
        To generate your dynamic QR code on your front end you will need the shareURL and SDK ID from your application.
    </div>
    <div class="alert-links"> 
        <a target="_self" href="https://developers.yoti.com/yoti/web-integration#modal">See here for all the QR types</a>
   </div>
</div>
{% /html %}

**Retrieving an credential**

Once the user has scanned the Yoti QR code, Yoti will perform a GET request to the defined call-back URL, passing a token as a query string parameter, any additional relying party defined query parameters will also be passed here.

{% html %}
<div class="alert-BYS">
   <div class="alert-title" id="BYS">
      Before you start
   </div>
   <div class="alert-text" >
      Please get familiar with our user profile service with the Yoti App.
   </div>
   <div class="alert-links"> 
           <a href="https://developers.yoti.com/yoti/web-integration#retrieve-a-profile">Retrieve a profile</a>
   </div>
</div>
{% /html %}

{% code %}
{% tab language="javascript" %}
COMING SOON
{% /tab %}
{% tab language="ruby" %}
COMING SOON
{% /tab %}
{% tab language="csharp" %}
profile.GetAttributeByName<string>(name: "_thirdPartyAttributeName"); //text/string
profile.GetAttributeByName<Dictionary<string, JToken>>(name: "_thirdPartyAttributeName"); //application/json
profile.GetAttributeByName<PngImage>(name: "_thirdPartyAttributeName"); //image/png
profile.GetAttributeByName<JpegImage>(name: "_thirdPartyAttributeName"); //image/jpeg
profile.GetAttributeByName<DateTime>(name: "_thirdPartyAttributeName"); //DateTime
profile.GetAttributeByName<int>(name: "_thirdPartyAttributeName"); //integer
{% /tab %}
{% tab language="python" %}
COMING SOON
{% /tab %}
{% tab language="java" %}
COMING SOON
{% /tab %}
{% tab language="go" %}
COMING SOON
{% /tab %}
{% tab language="php" %}
COMING SOON
{% /tab %}
{% /code %}

**Updating a credential**

You can update an individual users credential by overriding the value and using the issuance token associated to the user.  This requires no interaction from the user and will automatically update the Yoti app.

{% code %}
{% tab language="javascript" %}
const payload = new Payload({
    issuance_token: attributeIssuanceDetails.getToken(),
    name: 'com.example.someAttribute',
    value: 'some updated attribute value',
});

const request = new RequestBuilder()
    .withBaseUrl('https://api.yoti.com/api/v1/attribute-registry')
    .withEndpoint('/attribute/update')
    .withPemString('PEM_CONTENT')
    .withHeader('X-Yoti-Auth-Id', 'CLIENT_SDK_ID')
    .withMethod('PUT')
    .withPayload(payload)
    .build();

const response = await request.execute();
{% /tab %}
{% tab language="ruby" %}
payload = {
  issuance_token: attribute_issuance_details.token,
  name: 'com.example.someAttribute',
  value: 'some updated attribute value'
}

request = Yoti::Request
          .builder
          .with_base_url('https://api.yoti.com/api/v1/attribute-registry')
          .with_http_method('PUT')
          .with_endpoint('attribute/update')
          .with_payload(payload)
          .with_header('X-Yoti-Auth-Id', Yoti.configuration.client_sdk_id)
          .build

response = request.execute
{% /tab %}
{% tab language="csharp" %}
var dynamicScenarioBuilder = new DynamicScenarioBuilder();
var dynamicPolicyBuilder = new DynamicPolicyBuilder();

object deserializedObject;
using (StreamReader r = System.IO.File.OpenText("UpdateValue.json"))
{
	string text = r.ReadToEnd();
	deserializedObject = JsonConvert.DeserializeObject(text);
}

string attributeValueJson = JsonConvert.SerializeObject(deserializedObject);

string base64AttributeValue = Convert.ToBase64String(
	Encoding.UTF8.GetBytes(attributeValueJson));

string json = JsonConvert.SerializeObject(new
{
	issuance_token = _issuanceToken,
	name = _thirdPartyAttributeName,
	value = base64AttributeValue
});

byte[] httpContent = System.Text.Encoding.UTF8.GetBytes(json);

var signedRequest = new RequestBuilder()
	.WithBaseUri(new Uri("https://api.yoti.com/api/v1/attribute-registry"))
	.WithEndpoint("/attribute/update")
	.WithHttpMethod(HttpMethod.Put)
	.WithHeader("X-Yoti-Auth-Id", _clientSdkId)
	.WithKeyPair(_keyPair)
	.WithContent(httpContent)
	.Build();

var result = signedRequest.Execute(_httpClient).Result;
{% /tab %}
{% tab language="python" %}
import json

from yoti_python_sdk.http import SignedRequest

payload_data = {
    "issuance_token": attribute_issuance_details.token,
    "name": 'com.example.someAttribute',
    "value": 'some updated attribute value'
}

payload_string = json.dumps(payload_data).encode()

signed_request = (
    SignedRequest
    .builder()
    .with_pem_file("/path/to/key.pem")
    .with_base_url("https://api.yoti.com/api/v1/attribute-registry")
    .with_endpoint("/attribute/update")
    .with_http_method("PUT")
    .with_header("X-Yoti-Auth-Id", "CLIENT_SDK_ID")
    .with_payload(payload_string)
    .build()
)

response = signed_request.execute()
{% /tab %}
{% tab language="java" %}
byte[] payload = ...; // Payload is JSON converted to byte array
 
SignedRequest signedRequest = SignedRequestBuilder.newInstance()
            .withKeyPair(YOUR_KEY_PAIR)
            .withBaseUrl("https://api.yoti.com/api/v1/attribute-registry")
            .withEndpoint("/attribute/update")
            .withHttpMethod("PUT")
            .withPayload(payload)
            .build();
 
// 'SomeModel' is a POJO that has been defined by the user and is
// used to map JSON response as the SDK doesn't have any built in
// classes to support this
SomeModel someModel = signedRequest.execute(SomeModel.class);
 
/**
 * SignedRequest.execute() uses built in Java HTTP connectivity.
 * To use another framework if required (e.g. apache), you can get
 * all of the pieces of the Yoti signed request off the SignedRequest
 * object e.g.
**/
URI uri = signedRequest.getUri();
String httpMethod = signedRequest.getMethod();
byte[] payloadData = signedRequest.getData();
Map<String, String> headers = signedRequest.getHeaders();
{% /tab %}
{% tab language="go" %}
type Payload struct {
	Token string `json:"issuance_token"`
	Name  string `json:"name"`
	Value string `json:"value"`
}

body, err := json.Marshal(Payload{
	Token: issuingAttributes.Token(),
	Name:  "com.example.someAttribute",
	Value: "some attribute value",
})
if err != nil {
	panic(err)
}

headers := map[string][]string{
	"X-Yoti-Auth-Id": {"CLIENT_SDK_ID"},
}

decodedKey, err := cryptoutil.ParseRSAKey(key)
if err != nil {
	panic(err)
}

request, err := requests.SignedRequest{
	Key:        decodedKey,
	HTTPMethod: http.MethodPut,
	BaseURL:    "https://api.yoti.com/api/v1/attribute-registry",
	Endpoint:   "/attribute/update",
	Headers:    headers,
	Body:       body,
}.Request()
if err != nil {
	panic(err)
}

response, err := requests.Execute(&http.Client{}, request)
{% /tab %}
{% tab language="php" %}
<?php

use Yoti\Http\Payload;
use Yoti\Http\RequestBuilder;

$payload = Payload::fromJsonData((object) [
    'issuance_token' => $attributeIssuanceDetails->getToken(),
    'name' => 'com.example.someAttribute',
    'value' => 'some updated attribute value',
]);

$request = (new RequestBuilder())
    ->withBaseUrl('https://api.yoti.com/api/v1/attribute-registry')
    ->withEndpoint('/attribute/update')
    ->withPemFilePath('/path/to/key.pem')
    ->withHeader('X-Yoti-Auth-Id', 'CLIENT_SDK_ID')
    ->withMethod('PUT')
    ->withPayload($payload)
    ->build();

$response = $request->execute();

// Note:
// - Use RequestBuilder::withPemFile() to provide a `\Yoti\Util\PemFile`
// - Use RequestBuilder::withPemString() to provide PEM string
{% /tab %}
{% /code %}

**Revoking a credential**

You can revoke a credential from a users profile using the issuance token.  This requires no interaction from the user and will automatically update the Yoti app. The user will no longer be able to share or use the Yoti credential.

{% code %}
{% tab language="javascript" %}
const payload = new Payload({
    issuance_token: attributeIssuanceDetails.getToken(),
    name: 'com.example.someAttribute',
});

const request = new RequestBuilder()
    .withBaseUrl('https://api.yoti.com/api/v1/attribute-registry')
    .withEndpoint('/attribute/revoke')
    .withPemString('PEM_CONTENT')
    .withHeader('X-Yoti-Auth-Id', 'CLIENT_SDK_ID')
    .withMethod('PUT')
    .withPayload(payload)
    .build();

const response = await request.execute();
{% /tab %}
{% tab language="ruby" %}
payload = {
  issuance_token: attribute_issuance_details.token,
  name: 'com.example.someAttribute'
}

request = Yoti::Request
          .builder
          .with_base_url('https://api.yoti.com/api/v1/attribute-registry')
          .with_http_method('PUT')
          .with_endpoint('attribute/revoke')
          .with_payload(payload)
          .with_header('X-Yoti-Auth-Id', Yoti.configuration.client_sdk_id)
          .build

response = request.execute
{% /tab %}
{% tab language="csharp" %}
var dynamicScenarioBuilder = new DynamicScenarioBuilder();
var dynamicPolicyBuilder = new DynamicPolicyBuilder();

string json = JsonConvert.SerializeObject(new
{
	issuance_token = _issuanceToken,
	name = _thirdPartyAttributeName
});

byte[] httpContent = System.Text.Encoding.UTF8.GetBytes(json);

var signedRequest = new RequestBuilder()
	.WithBaseUri(new Uri("https://api.yoti.com/api/v1/attribute-registry"))
	.WithEndpoint("/attribute/revoke")
	.WithHttpMethod(HttpMethod.Put)
	.WithHeader("X-Yoti-Auth-Id", _clientSdkId)
	.WithKeyPair(_keyPair)
	.WithContent(httpContent)
	.Build();

var result = signedRequest.Execute(_httpClient).Result;
{% /tab %}
{% tab language="python" %}
import json

from yoti_python_sdk.http import SignedRequest

payload_data = {
    "issuance_token": attribute_issuance_details.token,
    "name": 'com.example.someAttribute',
}

payload_string = json.dumps(payload_data).encode()

signed_request = (
    SignedRequest
    .builder()
    .with_pem_file("/path/to/key.pem")
    .with_base_url("https://api.yoti.com/api/v1/attribute-registry")
    .with_endpoint("/attribute/revoke")
    .with_http_method("PUT")
    .with_header("X-Yoti-Auth-Id", "CLIENT_SDK_ID")
    .with_payload(payload_string)
    .build()
)

response = signed_request.execute()
{% /tab %}
{% tab language="java" %}
byte[] payload = ...; // Payload is JSON converted to byte array
 
SignedRequest signedRequest = SignedRequestBuilder.newInstance()
            .withKeyPair(YOUR_KEY_PAIR)
            .withBaseUrl("https://api.yoti.com/api/v1/attribute-registry")
            .withEndpoint("/attribute/revoke")
            .withHttpMethod("PUT")
            .withPayload(payload)
            .build();
 
// 'SomeModel' is a POJO that has been defined by the user and is
// used to map JSON response as the SDK doesn't have any built in
// classes to support this
SomeModel someModel = signedRequest.execute(SomeModel.class);
 
/**
 * SignedRequest.execute() uses built in Java HTTP connectivity.
 * To use another framework if required (e.g. apache), you can get
 * all of the pieces of the Yoti signed request off the SignedRequest
 * object e.g.
**/
URI uri = signedRequest.getUri();
String httpMethod = signedRequest.getMethod();
byte[] payloadData = signedRequest.getData();
Map<String, String> headers = signedRequest.getHeaders();
{% /tab %}
{% tab language="go" %}
type Payload struct {
	Token string `json:"issuance_token"`
	Name  string `json:"name"`
}

body, err := json.Marshal(Payload{
	Token: issuingAttributes.Token(),
	Name:  "com.example.someAttribute",
})
if err != nil {
	panic(err)
}

headers := map[string][]string{
	"X-Yoti-Auth-Id": {"CLIENT_SDK_ID"},
}

decodedKey, err := cryptoutil.ParseRSAKey(key)
if err != nil {
	panic(err)
}

request, err := requests.SignedRequest{
	Key:        decodedKey,
	HTTPMethod: http.MethodPut,
	BaseURL:    "https://api.yoti.com/api/v1/attribute-registry",
	Endpoint:   "/attribute/revoke",
	Headers:    headers,
	Body:       body,
}.Request()
if err != nil {
	panic(err)
}

response, err := requests.Execute(&http.Client{}, request)
{% /tab %}
{% tab language="php" %}
<?php

use Yoti\Http\Payload;
use Yoti\Http\RequestBuilder;

$payload = Payload::fromJsonData((object) [
    'issuance_token' => $attributeIssuanceDetails->getToken(),
    'name' => 'com.example.someAttribute',
]);

$request = (new RequestBuilder())
    ->withBaseUrl('https://api.yoti.com/api/v1/attribute-registry')
    ->withEndpoint("/attribute/revoke")
    ->withPemFilePath('/path/to/key.pem')
    ->withHeader('X-Yoti-Auth-Id', 'CLIENT_SDK_ID')
    ->withMethod('PUT')
    ->withPayload($payload)
    ->build();

$response = $request->execute();

// Note:
// - Use RequestBuilder::withPemFile() to provide a `\Yoti\Util\PemFile`
// - Use RequestBuilder::withPemString() to provide PEM string
{% /tab %}
{% /code %}