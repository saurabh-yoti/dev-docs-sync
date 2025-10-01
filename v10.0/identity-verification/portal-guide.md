---
type: page
title: Set up
listed: true
slug: portal-guide
description: 
index_title: Set up
hidden: 
keywords: 
tags: 
---

Yoti provides a portal that allows you to use our Identity verification service without doing any technical integration.

You will be able to create Identity verification sessions to send to your customers using our new user friendly product without using a line of code!

To get set up you will need to follow these steps:

1. Set up an account on the [Hub](https://hub.yoti.com/)
2. Register an organisation and get verified.
3. [Create an application](/identity-verification/portal-guide#create-an-application) and choose your configuration setup.
4. Log on to the [portal](https://identity.yoti.com/iam/login)

The below will guide you through step by step on how to get set up.

{% badge type="warning" text="Help" /%} If you need any help please contact us through our [support form](https://support.yoti.com/yotisupport/s/contactsupport)

---

### Supported Browsers

{% image url="https://image-archive.developerhub.io/image/upload/71142/rstg3qyxjlhzssaeqjfm/1603187142.png" caption="Supported browsers" mode="600" height="216" width="688" %}
{% /image %}

---

Register with the Yoti Hub

1. **[Open Yoti Hub](https://hub.yoti.com)** on a desktop or laptop.
2. Create an account
3. Complete the organisation registration on Yoti Hub.

{% html %}
<div class="alert-BYS">
   <div class="alert-title" id="BYS">
      Jump to
   </div>
   <div class="alert-text" >
      For a step by step guide on how to onboard with the hub head over to the Getting started section.
   </div>
   <div class="alert-links"> 
      <a  target="_self" href="https://developers.yoti.com/yoti/getting-started
                               "> Onboarding with Yoti </a>
   </div>
</div>
{% /html %}

---

## Create a service

Here you will to create an Identity verification application in your Yoti Hub. To create your service:-

- Click the **services** tab in the side menu.
- Choose which product you would like to integrate with, select **Identity verification:**

{% image url="https://uploads.developerhub.io/prod/kvAX/20nkwnajq0s2r8hkbpvk9low9espj9k0ywj34618x0zejtz3ew9dadzpsfbd4gek.png" mode="responsive" height="1014" width="2398" %}
{% /image %}

- After pressing **Continue**, click on the No-Code(Yoti Portal) option:

{% image url="https://uploads.developerhub.io/prod/kvAX/n25r6i3taoec840qmqtcr9bhp7g8kd0yhqew6ga1mtt61nzt0h9xeqwekk4dztai.png" mode="responsive" height="1118" width="2286" %}
{% /image %}

- Fill in the Details tab - including your service name, then click **Create**.

{% table widths="" %}
| Details | Explained | 
| ---- | ---- | 
| Service Name | This is the name of your service in the hub and is used to differentiate between each service in the portal. | 
| Technical contact (optional) | This is the contact Yoti can contact you for changes, updates and feedback. | 
{% /table %}

You will now see the following screen:

{% image url="https://uploads.developerhub.io/prod/kvAX/0i9sabztg4lozfpqvhs9illr6gmxbudm4igwxl4mmziwsc8oq5xlnhx5s4qwoqua.png" mode="responsive" height="1192" width="2398" %}
{% /image %}

### Choose your configuration set up

Before you start here get familiar with our user view. See what your users would go through by using the following [demo](https://yoti.world/yoti-idv/).

You will be provided with a list of checks that Identity verification provides. 

- Click on **portal preferences.**
- Please tick which checks and tasks you wish to have as part of your user sessions. 

A session represents one end-to-end use of the ID verification service. Each time the ID verification service is initiated (regardless of which specific tasks/checks are required) a new session is created.

{% image url="https://image-archive.developerhub.io/image/upload/v2_2762/gxp0hzqjoiuo2zhpqvvd/1636396942.png" caption="Creating a service &gt; Portal Preferences" mode="responsive" height="1158" width="1482" %}
{% /image %}

Below describes the multiple checks Yoti provides for identity verification. We offer a manual check for most of the checks. If you require a manual check please select the following as part of your check:-

{% table widths="" %}
| Check type | Description | 
| ---- | ---- | 
| Always | The requested check will always get manually check regardless of the success of the automated check. | 
| Never | The requested check will never get manual checked. | 
| Fallback | The requested check will be manually checked if the automated check fails. | 
{% /table %}

You can select your preference in within each tick box check. 

### Checks explained

If you understand what checks you want, you can skip this section. 

{% table widths="" %}
| Name | Manual check available | 
| ---- | ---- | 
| Liveness check | ❌ | 
| Document authenticity | ✅ | 
| Text extraction | ✅ | 
| Face match check | ✅ | 
| Supporting documents | ✅ | 
| Document comparison | ❌ | 
| Address check | ✅ | 
| AML check | ❌ | 
{% /table %}