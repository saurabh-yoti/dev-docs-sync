---
type: page
title: Tracked Devices
listed: true
slug: tracked-devices
description: 
index_title: Tracked Devices
hidden: 
keywords: 
tags: 
---

Yoti offers the ability to request the devices that interacted with the session and some of the devices details. We record this metadata once specific events in the user journey have occurred. An object will be generated per each event, detailing the device information at the time of the event.

{% code %}
{% tab language="javascript" title="Node.js" %}
const devicesResponse = await idvClient.getSessionTrackedDevices(sessionId);
const events = devicesResponse.getDeviceEvents()
const firstEvent = events[0]

firstEvent.getEvent();  
firstEvent.getCreated();  

const firstEventDevice = firstEvent.getDevice();   

firstEventDevice.getIpAddress();  
firstEventDevice.getManufactureName();  
firstEventDevice.getModelName();  
firstEventDevice.getOSName();  
firstEventDevice.getOSVersion();  
firstEventDevice.getBrowserName();  
firstEventDevice.getBrowserVersion();  
firstEventDevice.getLocale();  
firstEventDevice.getClientVersion();
{% /tab %}
{% tab language="php" %}
<?php
use Yoti\Http\RequestBuilder;
use Yoti\Http\Payload;
$request = (new RequestBuilder())
    ->withBaseUrl('https://api.yoti.com/idverify/v1')
    ->withPemFilePath('<YOTI_KEY_FILE_PATH>')
    ->withEndpoint('/sessions/<session_ID>/tracked-devices')
    ->withMethod('GET')
    ->withQueryParam('sdkId', '<YOTI_CLIENT_SDK_ID>')
    ->build()
    //get Yoti Response
    ->execute();
{% /tab %}
{% /code %}

{% table widths="247" %}
| Event | Description | 
| ---- | ---- | 
| CONFIG_FIRST_LOADED | The user has successfully landed on the starting screen. | 
| RESOURCE_CREATED | A resource has successfully been created. e.g a document image has been captured. | 
| CLIENT_SESSION_TOKEN_DELETED | User journey has been completed. | 
{% /table %}

#### Example Response

{% code %}
{% tab language="json" %}
[
    {
        "event": "CONFIG_FIRST_LOADED",
        "created": "2024-07-24T14:15:06Z",
        "device": {
            "ip_address": "",
            "manufacture_name": "Apple",
            "model_name": "Macintosh",
            "os_name": "Mac OS",
            "os_version": "10.15.7",
            "browser_name": "Chrome",
            "browser_version": "126.0.0.0",
            "locale": "en-GB",
            "client_version": ""
        }
    },
    {
        "event": "RESOURCE_CREATED",
        "resource_id": "a10cce10-c497-4011-8eab-4759e1f6fe49",
        "created": "2024-07-24T14:15:10Z",
        "device": {
            "ip_address": "",
            "manufacture_name": "Apple",
            "model_name": "Macintosh",
            "os_name": "Mac OS",
            "os_version": "10.15.7",
            "browser_name": "Chrome",
            "browser_version": "126.0.0.0",
            "locale": "en-GB",
            "client_version": ""
        }
    },
    {
        "event": "CLIENT_SESSION_TOKEN_DELETED",
        "created": "2024-07-24T14:15:55Z",
        "device": {
            "ip_address": "",
            "manufacture_name": "Apple",
            "model_name": "Macintosh",
            "os_name": "Mac OS",
            "os_version": "10.15.7",
            "browser_name": "Chrome",
            "browser_version": "126.0.0.0",
            "locale": "en-GB",
            "client_version": ""
        }
    }
]
{% /tab %}
{% /code %}

These device details can also be deleted by using the below method:

{% code %}
{% tab language="javascript" title="Node.js" %}
await idvClient.deleteSessionTrackedDevices(sessionId);
{% /tab %}
{% tab language="php" %}
<?php
use Yoti\Http\RequestBuilder;
use Yoti\Http\Payload;
$request = (new RequestBuilder())
    ->withBaseUrl('https://api.yoti.com/idverify/v1')
    ->withPemFilePath('<YOTI_KEY_FILE_PATH>')
    ->withEndpoint('/sessions/<session_ID>/tracked-devices')
    ->withMethod('DELETE')
    ->withQueryParam('sdkId', '<YOTI_CLIENT_SDK_ID>')
    ->build()
    //get Yoti Response
    ->execute();
{% /tab %}
{% /code %}