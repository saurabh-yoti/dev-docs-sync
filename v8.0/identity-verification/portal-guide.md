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

1. Set up an account on the [Hub](https://hub.yoti.com/login-organisations)
2. Register an organisation and get verified.
3. [Create an application](/identity-verification/portal-guide#create-an-application) and choose your configuration setup.
4. Log on to the [portal](https://identity.yoti.com/iam/login)

The below will guide you through step by step on how to get set up.

{% badge type="warning" text="Help" /%} If you need any help please email [clientsupport@yoti.com](mailto:clientsupport@yoti.com).

---

### Supported Browsers

{% image url="https://image-archive.developerhub.io/image/upload/71142/rstg3qyxjlhzssaeqjfm/1603187142.png" caption="Supported browsers" mode="600" height="216" width="688" %}
{% /image %}

---

Register with the Yoti Hub

1. **[Open Yoti Hub](https://hub.yoti.com/login-organisations)** on a desktop or laptop.
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

## Create an application

Here you will to create an Identity verification application in your Yoti Hub. To create your application:-

- Click the **applications** tab in the side menu.
- Choose which product you would like to integrate with, select **Identity verification:**

{% image url="https://image-archive.developerhub.io/image/upload/v2_2762/celvi0kcxavscpr5sbkc/1623406298.png" caption="Create an application" mode="responsive" height="1358" width="1734" %}
{% /image %}

- After pressing **Proceed**
- Fill in the Details tab - including your application name and logo, then click **Create**.

{% table %}
| Details | Explained | 
| ---- | ---- | 
| Application Name | This is the name of your application in the hub and is used to differentiate between each application in the portal. | 
| Technical contact (optional) | This is the contact Yoti can contact you for changes, updates and feedback. | 
{% /table %}

You will now see the following screen:

{% image url="https://image-archive.developerhub.io/image/upload/v2_2762/ztlnwpmvfn2wed1cfxdk/1623406385.png" caption="Creating an application &gt; Keys" mode="responsive" height="1338" width="1788" %}
{% /image %}

- Click on the **Keys** tab
- Click the Generate keys button, you will be asked whether you want to store the keys.  Click this checkbox and the keys will automatically be managed by Yoti on your behalf. 

{% image url="https://image-archive.developerhub.io/image/upload/v2_2762/ioqxjxe7akliwhm4ubbc/1636396903.png" caption="Creating an application &gt; Keys &gt; Tick box" mode="responsive" height="1174" width="1054" %}
{% /image %}

If you ever decide that you no longer want Yoti to store your keys, you will be able to regenerate your keys and uncheck the checkbox.  This will prevent you or your users from being able to view existing data in the portal.

### Choose your configuration set up

Before you start here get familiar with our user view. See what your users would go through by using the following [demo](https://yoti.world/yoti-idv/).

You will be provided with a list of checks that Identity verification provides. 

- Click on **portal preferences.**
- Please tick which checks and tasks you wish to have as part of your user sessions. 

A session represents one end-to-end use of the ID verification service. Each time the ID verification service is initiated (regardless of which specific tasks/checks are required) a new session is created.

{% image url="https://image-archive.developerhub.io/image/upload/v2_2762/gxp0hzqjoiuo2zhpqvvd/1636396942.png" caption="Creating an application &gt; Portal Preferences" mode="responsive" height="1158" width="1482" %}
{% /image %}

Below describes the multiple checks Yoti provides for identity verification. We offer a manual check for most of the checks. If you require a manual check please select the following as part of your check:-

{% table %}
| Check type | Description | 
| ---- | ---- | 
| Always | The requested check will always get manually check regardless of the success of the automated check. | 
| Never | The requested check will never get manual checked. | 
| Fallback | The requested check will be manually checked if the automated check fails. | 
{% /table %}

You can select your preference in within each tick box check. 

### Checks explained

If you understand what checks you want, you can skip this section. 

{% table %}
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