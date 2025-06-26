---
type: page
title: Portal View
listed: true
slug: portal-view
description: 
index_title: Portal View
hidden: 
keywords: 
tags: 
---

Yoti provides a portal that allows you to view the results of your checks.

To get set up you will need to follow these steps:

1. Set up an account on the [Hub](https://hub.yoti.com/login-organisations)
2. Add yourself as a portal user to your age verification application
3. Log on to the [portal](https://identity.yoti.com/iam/login)

The below will guide you through step by step on how to get set up.

{% badge type="warning" text="Help" /%} If you need any help please email [clientsupport@yoti.com](mailto:clientsupport@yoti.com).

---

#### Add users

To add a user to your portal:

- Login to the Yoti hub
- Select your age verification application
- Go to the **portal users** tab

{% image url="https://uploads.developerhub.io/prod/kvAX/0y5fwksx8hwhytuy2beanfig4vzsgacz2ueu4px0e29g4aalsc970qypcjquyj34.png" mode="responsive" height="918" width="1920" %}
{% /image %}

- Click add user
- Type in the person’s email address.
- Once you add a user, they will get emailed a link to the portal and will need to create an account on the portal.

All users will receive an email from Yoti. They will then need to register on the portal at [https://identity.yoti.com/iam/create](https://identity.yoti.com/iam/create). The new users will be guided through this via the email they receive.

You can edit a users permission to be able to just view the result of the checks or to also be able to view the details of the check.

{% image url="https://uploads.developerhub.io/prod/kvAX/czmd5dm0e5l0vri0iwx4xqxkx3x6meyenckzalkzq5oiex4iaw1z4bc4iujqi2rl.png" mode="responsive" height="424" width="409" %}
{% /image %}

---

#### Login

Once you have set your preferences you can now begin using the portal. If you have added yourself to the application created above you should receive an email directing you to the portal.

Log in URL: [https://identity.yoti.com/](https://identity.yoti.com/)

Create an account or scan the QR code. Your email address should be the same as what you inputted in your application.

All users are required to set up 2 factor authentication to access the portal, This can either be done as part of one step when using the Yoti app or a popular authentication app such as Google Authenticator or Authy.

Your home page will be a list of applications, click the relevant Age verification application. If this is your first time using the product there will only be one.

---

#### Log out

To log out of the portal click the menu button in the top right corner of the page and click on the log out button. If you do not log out your account will stay logged in for 24 hours until it auto logs you out.

{% image url="https://uploads.developerhub.io/prod/kvAX/swyy9721m2gucayhqd8ap2x5590zdz7fas9ggyockuy61cbwro25uhqufqlv6qwh.png" mode="responsive" height="518" width="428" %}
{% /image %}

---

#### Session Results

Once logged in you will see a dashboard with all the sessions that have already been created or completed:

{% image url="https://uploads.developerhub.io/prod/kvAX/sqxau0z9yrhin7kv1eunnzpytncprmh1jux25i5mlhz9274251t3b1wuqglnpfgs.png" mode="responsive" height="981" width="1920" %}
{% /image %}

The statuses are related to the below reasons:

{% table widths="126" %}
| Status | Description | 
| ---- | ---- | 
| Complete | The session has been completed, the user has passed the required threshold or an age has been returned. | 
| Fail | The session has been completed, however the user has failed to meet the age threshold. FAIL will be returned only for 'OVER' and 'UNDER' attempts. | 
| Pending | User has not started any checks. | 
| In progress | Checks have begun on the session, awaiting result to be returned. | 
{% /table %}

You can get a breakdown of the result by clicking into the tab:

{% image url="https://uploads.developerhub.io/prod/kvAX/f8zj6jcqp5cnq4qpsymt0c138wy3x6f2jaef2nbyisr997xk6zhm7643w2g0ucyb.png" mode="responsive" height="980" width="1920" %}
{% /image %}