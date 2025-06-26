---
type: page
title: Notifications
listed: true
slug: notifications
description: 
index_title: Notifications
hidden: 
keywords: 
tags: 
---

Each session has a configured 'time to live' (TTL) which must be above 60 seconds (1 minute). When a session is created, it remains active until it's time to live is reached.

To receive the result of an age verification, a HTTP endpoint (notification URL) needs to be listening for a JSON payload in the format of the below through a POST method. 

Notifications require HTTPS and will be reattempt if a 200 status code is not received. It is important to acknowledge the notification with a 200 status code to avoid receiving repeat notifications.

Below is an example payload:

{% code %}
{% tab language="json" %}
{
  "method": "AGE_ESTIMATION",
  "result": false,
  "age": 30,
  "session_key": "69db8ad4-c983-40b3-b95a-a8fa576e70a6",
  "reference_id": "some_reference_id",
  "id": "2480375e-ddc0-4832-9b82-b1d14af5cf75",
  "timestamp": 1613482863,
  "notification_url": "https://mynotification.example.com",
  "evidence_id": "da4070de-3d34-44d7-86d4-7d6fdf547740",
  "state": "FAIL",
  "check_type": "NONE",
  "sequence_number": 1,
  "signature": "some_signature"
}
{% /tab %}
{% /code %}

{% table %}
| Field | Value | Description | 
| ---- | ---- | ---- | 
| method | AGE_ESTIMATION\n\n\n\nDOC_SCAN\n\n\n\nDIGITAL_ID | The method used to complete the Age verification session. | 
| result | true\n\n\n\nfalse | The result is true if the user met the OVER or UNDER criteria, false if not. The result is always true for type of AGE when an age is returned. | 
| age | integer | Returns the actual age if type AGE. Otherwise returns the threshold value. | 
| session_key | uuid | The Age verification session ID. | 
| reference_id | string | The reference_id submitted to the session create endpoint is returned in this field. | 
| id | uuid | Notification ID. | 
| timestamp | epoch timestamp | Timestamp for when the notification was sent. | 
| notification_url | string | The notification_url submitted to the session create endpoint is returned in this field. | 
| evidence_id | uuid | An ID relating to a specific Age verification attempt. | 
| state | FAIL\n\n\n\nCOMPLETE\n\n\n\nERROR | FAIL - The session has been completed, however the user has failed to meet the age threshold. FAIL will be returned only for 'OVER' and 'UNDER' attempts.\n\n\nCOMPLETE - The session has been completed, the user has passed the required threshold or an age has been returned.\n\n\nERROR - We could not provide an age result or calculate the threshold. This may be because the face was not recognised during age estimation or the ID document could not be processed through Doc Scan.\n\n\nAdditional states may be added in future releases and therefore mapping methods should contain default values. | 
| check_type | NONE\n\n\n\nPASSIVE | Returns the type of liveness check that was performed in the Age verification session. This is specified as the 'level' at session creation. | 
| sequence_number | integer | The attempt number for the current notification. Starts at 1. | 
| signature | string | Signed notification payload which can be verified using the Age verification public key. | 
{% /table %}

## Verifying the Signature

Within the notification object, Yoti returns a signature, this allows you to verify that the notification originated from Yoti's Age Verification service.

Verifying the signature may be achieved by:

1. Creating a JSON string from the notification payload, stripping out `sequence_number` and `signature`. All spaces in this string must be trimmed.
2. Convert the resulting JSON string into bytes.
3. Hash these bytes using SHA256.
4. RSA-SHA256 verify the hash of the bytes returned from Step 3, to the byte value of the signature in the webhook response.

The public is at the bottom of this page.

**Note:** Notifications are optional, and our recommendation is to use them when asynchronous age checks (for example via ID document) are used. For methods that immediately return a result immediately, such as Digital ID & Age estimation, the session result may be fetched from the [results](/age-verification/results) endpoint.

### Example code

{% code %}
{% tab language="javascript" %}
const crypto = require("crypto");
const fs = require('fs');

// Load the public key from a local file
const publicKeyPath = 'keys/public-key.pem';
const publicKey = fs.readFileSync(publicKeyPath, 'utf-8');

function verify(publicKey, signature, payload) {
  const verifier = crypto.createVerify("RSA-SHA256");
  verifier.update(payload);

  return verifier.verify(
    { key: publicKey, padding: crypto.constants.RSA_PKCS1_PSS_PADDING },
    Buffer.from(signature, 'base64')
  );
}

// Notification JSON
const data = { /* your data here */ };

const { sequence_number, signature, ...payload } = data;
const verified = verify(publicKey, signature, JSON.stringify(payload).replace(/\s/g, ''));

console.log('Signature Verified: ', verified);
{% /tab %}
{% tab language="java" %}
// Coming soon
{% /tab %}
{% tab language="php" %}
<?php

// Include the Composer autoload file
require __DIR__ . '/vendor/autoload.php'; 

// Use the Phpseclib3 library
use phpseclib3\Crypt\RSA;

// Load the public key from a local file
$publicKeyPath = 'keys/public-key.pem';
$publicKey = RSA::loadPublicKey(file_get_contents($publicKeyPath));

// Notification JSON String
$jsonData = '{ ... }';

// Decode the JSON data
$data = json_decode($jsonData, true);

// Remove 'sequence_number' and 'signature' from the data
unset($data['sequence_number']);
$signature = $data['signature'];
unset($data['signature']);

// Convert the modified JSON data back to a JSON string and remove spaces
$jsonString = json_encode($data, JSON_UNESCAPED_UNICODE | JSON_UNESCAPED_SLASHES);
$jsonString = str_replace(' ', '', $jsonString);

// Decode the signature
$signatureDecoded = base64_decode($signature);

// Determine the signature length in bytes
$signatureLengthBytes = strlen($signatureDecoded);

// Set the digest output length
$digestOutputLength = 32;

// Calculate the salt length
$saltLength = $signatureLengthBytes - $digestOutputLength - 2;

// Verify the signature using the public key
$verified = $publicKey
    ->withPadding(RSA::SIGNATURE_PSS)
    ->withHash('sha256')
    ->withSaltLength($saltLength)
    ->verify($jsonString, $signatureDecoded);

if ($verified) {
    echo 'Signature Verified: true';
} else {
    echo 'Signature Verified: false';
}
{% /tab %}
{% /code %}

{% code %}
{% tab language="markdown" title="Public Key" %}
-----BEGIN PUBLIC KEY-----
MIIBojANBgkqhkiG9w0BAQEFAAOCAY8AMIIBigKCAYEAune8+8vPz/pQD6IzdWvX
Q66nh/RcywopCI01Wjo6i7vlH2iVOP1oCkgbObe12iMmVXKRiXgMNT6aXIGe6Ggw
dodzAmt3vT1fmrgub7Of6MgJ56ri2uH1O54DTjbnEbEcLXX13teOusZavntrkNpp
x1c8L0Ol41mRvImJeMHM6I16rLhqB/w1m7USMvof/K6GaP+VmmciZTPyZ6IsXxvB
k0ZoqWqrt2xENlg4O6LXMo7eHEiG+edm9uDpbZK1RhiCd6hyDZ/t4bBQNg4misFF
WezQSiUlPwBLRg1AJ3CNrtBzs49BZ30U7WSPUS0Gsq1lhhDtUtJUt4CdkDAfkVY6
2C6aaqKV940GcPFN7MjOeFus3VNJE3zyHVLT8DStuLMXHY+gQBGFOyxN6heZbm7a
Sl9fi7VXlDTlv1jpk4DFMQYF2fpAyomm95GavhllJnDxC2t8ebu0O23B88hPGI3K
kyLtPA8ie6UNmwNqLYpOEN/pwayYw75FcENBDxnWhoe9AgMBAAE=
-----END PUBLIC KEY-----
{% /tab %}
{% /code %}