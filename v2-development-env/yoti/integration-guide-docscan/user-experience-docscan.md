---
type: page
title: User experience Dev
listed: true
slug: user-experience-docscan
description: 
index_title: User experience Dev
hidden: 
keywords: 
tags: 
---

Create optimal experiences for your customers and increase conversion by following these best practices for web and mobile integrations.

In this section, we offer tips and considerations to create a great and simple experience for your users.

{% html %}
<div class="alert-BYS">
   <div class="alert-title" id="BYS">
      Before you start
   </div>
   <div class="alert-text" >
      Have a look how Yoti integrations work
   </div>
   <div class="alert-links"> 
      <a target="_self" href="https://developers.yoti.com/yoti/technical-overview-docscan">See Integration guide</a> 
   </div>
</div>
{% /html %}

## General guidelines

We suggest people integrating with any Yoti products follow these suggestions

**1. Only ask for the information you need.**

We've found that people will be more likely to complete the process if they feel secure, and if they're being asked for a reasonable amount of details. For example, asking someone to scan their face when it won't provide any significant benefits may increase drop-off rate.

**2. Be transparent with your customers.**

When talking about identity details, keep your language simple and understandable. We've found that people are more likely to convert if they have confidence in what is happening to their data. We have plenty of examples of how to explain these differences on our website.

**3. Explain your relationship with Yoti**

As a third party company, it's important that your customers trust your faith in us. Be clear about how Yoti is helping you and in what ways. Showing that you trust Yoti will help people to share their identity details with confidence. There are specific pieces of information included in Yoti Doc Scan to help people understand how it works. In your own FAQs, mentioning Yoti will add reassurance that you trust them.

---

## Key user experience touchpoints

{% image url="https://res.cloudinary.com/developerhub/image/upload/v1575457104/23614/xfylyp8e1qwjhapnulyi.jpg" caption="Key touchpoints" mode="responsive" height="590" width="1490" %}
{% /image %}

### Before they start

Through multiple rounds of testing, we’ve found some easy ways to reassure people before they begin to prove their authenticity:

- Be transparent about where the information you're asking to collect is going to be stored and for how long.
- If you have an idea of how long the process will take let them know.
- If you're doing a document check, tell them that they will need to have an identity document to hand before they start.
- If you're doing a liveness check, let them know in advance that you'll need access to their camera to capture their face.
- Mention that you're using a trusted third party to perform the verification checks.

{% image url="https://res.cloudinary.com/developerhub/image/upload/v1575457277/23614/xme9hf2at0vkdpvyqj3v.jpg" caption="Before they start" mode="300" height="508" width="530" %}
{% /image %}

### During the process

Sending your personal details through a third party service can be an unnerving experience. We do all we can to ensure your customers’ comfort, but there are additional steps you can take to reassure them.

- Avoid interrupting someone whilst they're submitting their information. Mute things like notifications so they can remain focused.
- If you're embedding Yoti Doc Scan in a page, hide or remove any content around the iframe that might distract someone. Things like adverts could also unnerve users and affect their level of trust.
- Handle any errors correctly and consistently. We explain more about errors in detail in a couple of chapters.

{% image url="https://res.cloudinary.com/developerhub/image/upload/v1575457461/23614/lsvgekiygmtual28ufdb.jpg" caption="During the process" mode="300" height="498" width="528" %}
{% /image %}

### Waiting for approval

There will be a period of time after your customers submit their application where we’ll need to review their details. This process could take several minutes. During this time, you’ll need to keep your customer informed about the status of their application.

- Tell them that it could take a few minutes for the checks to be made.
- Give them an area where they can check the status of their application.
- When possible, allow them to continue using your service.

{% image url="https://res.cloudinary.com/developerhub/image/upload/v1575457542/23614/uenrwieidy4ejmj82jy3.jpg" caption="Waiting for approval" mode="300" height="552" width="570" %}
{% /image %}

### Getting the report

Once we’ve reviewed your customer’s application, you’ll be able to see the results of the check.

- If your customer has passed the check then let them know. This is best done either through email or via notifications if you use them.
- For customers who fail the check, give them an option to either try again or go through an alternative method.

{% image url="https://res.cloudinary.com/developerhub/image/upload/v1575457622/23614/u8s4hnysaohenla8q8a1.jpg" caption="Getting the report" mode="300" height="482" width="488" %}
{% /image %}

---

## Yoti Doc Scan Layouts

We have designed every screen within Yoti Doc Scan to work seamlessly across browser windows of any size.

{% image url="https://res.cloudinary.com/developerhub/image/upload/v1575457784/23614/zxe6phzse4kiexw3v6jl.jpg" caption="Yoti Doc scan layouts - Web and Mobile" mode="responsive" height="604" width="1316" %}
{% /image %}

**Web Layout**

Before we talk about breakpoints, it’s worth mentioning that we currently use two templates for content within Yoti Doc Scan. 

The common template is used for most screens. The main content takes up the full width of the modal. Primary navigation can be found in the bottom right or in the top left. Additional links can be located in the main content. 

The activity template is reserved for specifications that require more focus. For example, the document capture process is performed using this template. The main actionable area is found on the right-hand side; supporting guidance and helpful links are on the left-hand side.

{% image url="https://res.cloudinary.com/developerhub/image/upload/v1575457995/23614/zwz551ctyjd71bxbdn6x.jpg" caption="Web layout" mode="300" height="856" width="618" %}
{% /image %}

Depending on the size of the browser window, the Yoti Doc Scan frame will adapt to the space in a variety of ways.

For windows of width ≤628px the view on desktop will change the mobile web layout. For window sizes between 628px and 934px the frame contents will take on the desktop layouts, adapting to fit the space.

For windows of width ≥ 934px the frame will remain a fixed size. The frame will expand with a transparent background, allowing you to put whatever colour you’d like in the background.

{% image url="https://res.cloudinary.com/developerhub/image/upload/v1575458185/23614/tyniaij8kjoqjsjor0iu.jpg" caption="Breakpoints on desktop" mode="responsive" height="480" width="1460" %}
{% /image %}

**Mobile browser layout**

On mobile browsers we can only display content in a single column. This common template is used for all screens.

This screen will sit within the browser window. Your customer will still be able to navigate using the native controls (eg, go back, close tab). The primary action button can usually be found at the bottom of the window; otherwise, it will be clearly visible within the page content.

{% image url="https://res.cloudinary.com/developerhub/image/upload/v1575458062/23614/xq59mdypmzfxg8915uhf.jpg" caption="Mobile layout" mode="300" height="650" width="406" %}
{% /image %}

{% html %}
<div class="alert-GTK">
    <div class="alert-title" id="GTK">
        Jump to... 
    </div>
    <div class="alert-text">
        The config to create this session and launch the user view.
    </div>
    <div class="alert-links"> 
        <a href="https://developers.yoti.com/yoti/render-the-user-view">Launch the user view</a>
   </div>
</div>
{% /html %}

---

## Error handling

Throughout the Yoti Doc Scan process, your customers can encounter several types of errors. This is a quick guide on where these errors occur in the flow and how best to handle them.

There are several instances where someone can be forced out of the Yoti Doc Scan SDK; when this happens we’ll redirect to the error URL you provide in your configuration.

On this page, we suggest you provide the following:

- Reassurance that the fault is with the system, not them.
- Give them an easy way to begin the process again from the error page.
- Also give them an alternative way to prove their identity (eg, a video call with a customer support representative).

**Generic errors**

{% image url="https://res.cloudinary.com/developerhub/image/upload/v1575458496/23614/ivd3dhkqlwqhwsdrrns6.jpg" caption="Generic errors" mode="responsive" height="908" width="1492" %}
{% /image %}

{% table %}
| Reason for failure | Suggested action | 
| ---- | ---- | 
| They cancelled the session for an unknown reason. | Start the session again | 
| Their session was configured incorrectly. | Start the session again | 
| Something went wrong during a network request. | Check their connection and try again. | 
| There was a network error | Check their connection and try again. | 
| Their session timed out | Start the session again | 
| Your SDK is out of date | Try a different verification method. Update your SDK to the latest version. | 
{% /table %}

**Document capture errors**

{% image url="https://res.cloudinary.com/developerhub/image/upload/v1575458875/23614/pvp1xif5mhemrcb2vrcn.jpg" caption="Document capture check" mode="300" height="712" width="384" %}
{% /image %}

There are some specific errors that can only be thrown during the document capture process:

{% table %}
| Reason for failure | Suggested action | 
| ---- | ---- | 
| They did not grant permissions to the camera | Start the session again, They will be asked to grant permissions again. | 
| They do not have a camera on their device. | Try a different verification method. | 
| The document upload process failed too many times | Start the session again, or offer an alternative verification method. | 
{% /table %}

**Liveness check errors**

{% image url="https://res.cloudinary.com/developerhub/image/upload/v1575459355/23614/ilu7umlim0dsys2gceik.jpg" caption="Liveness check" mode="300" height="730" width="386" %}
{% /image %}

There are some specific errors that can only be thrown during the liveness process:

{% table %}
| Reason for failure | Suggested action | 
| ---- | ---- | 
| They did not grant permissions to the camera. | Start the session again. They will be asked to grant permissions again. | 
| They couldn't pass the liveness test. This is either due to user error or them attempting to spoof the check. | Try a different verification method. | 
| They do not have a camera on their device | Try a different verification method. | 
{% /table %}