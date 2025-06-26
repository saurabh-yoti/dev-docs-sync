---
type: page
title: Create a QR code application
listed: true
slug: create-a-qr-code-application
description: 
index_title: Create a QR code application
hidden: 
keywords: 
tags: 
---


Here you will create your QR code page.

1. Create a Digital ID application and scenario in the hub. Instructions can be found [here](/digital-id/production-keys).
1. You will select:

    1. The [auto$](/digital-id-legacy/yoti-attributes) that you wish to retrieve from the user.
    2. Customisation ability to change the logo and background of the QR code page.
    3. Please see detailed set up notes [here](https://app.developerhub.io/digital-id/production-keys).

2. Please set the domain to: [www.yoti.com](http://www.yoti.com/)
3. Please set the callback URL to: [www.yoti.com/connect/thankyou](http://www.yoti.com/connect/thankyou)
4. Lastly to retrieve the URL of your page:
    1. Head over to your scenario (Click **applications**, your application and you will see the **scenario** tab).
    2. Click the small arrow in the scenario and press **Edit**.


{% image url="https://uploads.developerhub.io/prod/kvAX/rjfo2z00ebtmrg5j2r6osns08dt10dpvz008fda3pklulzu0hc219nkzhrk5dtv1.png" caption="Edit your scenario" mode="responsive" height="557" width="1253" %}
{% /image %}


5. The URL will be at the top of this page. Copy this URL as it will be the page that users will land on to scan the QR code.

Please see this page as an [example](https://www.yoti.com/connect/32e513d2-4faa-4179-9c0a-cbbb1a673460/scenarios/97483364-1cf0-41cb-be80-bea4babecf78).

