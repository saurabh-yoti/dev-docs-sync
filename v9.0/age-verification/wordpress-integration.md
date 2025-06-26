---
type: page
title: WordPress Integration guide
listed: true
slug: wordpress-integration
description: 
index_title: WordPress
hidden: 
keywords: 
tags: 
---

{% callout type="info" title="Good to know" %}
This integration is in BETA. Please help us improve by providing feedback.

[Contact us](https://support.yoti.com)
{% /callout %}

Welcome to the documentation for integrating Yoti Age verification (AV) with WordPress.

Following are the integration steps:

1. Download the plugin
2. Install the plugin
3. Add your keys and configure the plugin options
4. Enable Age verification for relevant posts/pages

---

## Download the plugin

Download the plugin installation file from this [link](https://drive.google.com/drive/folders/1MLdD0h_rb5tAkkYFHpEeuGR2J7OvsZW_).

---

## Install the plugin

Head to your WordPress admin panel.

- Open Plugins page from the left menu
- Then, click the ‘**Add New Plugin**’ button

{% image url="https://uploads.developerhub.io/prod/kvAX/8ag2y8gr6sfrrzjkdhzpm2ykijjw9wj90x5mrsdpvx9afx5o2ba1fmi9n3c4ztkw.jpg" caption="Settings &gt; Plugins &gt; Add New Plugin" mode="responsive" height="816" width="1920" %}
{% /image %}

- After, click the ‘**Upload Plugin’** button
- Click the ‘**Choose file**’ button and select the plugin zip file
- Then click the **‘Install Now’** button

{% image url="https://uploads.developerhub.io/prod/kvAX/ipp19k49bxrt3pd057jn7k8eb11uw53lm14cftqdn805cvrjd6s612ayc8r7y65t.jpg" caption="Settings &gt; Plugins &gt; Add New Plugin &gt; Upload Plugin &gt; Install Now" mode="responsive" height="661" width="1920" %}
{% /image %}

- Finally, click on ‘Activate’ link below the installed plugin name

{% image url="https://uploads.developerhub.io/prod/kvAX/y1ngmcc9hqfqbjq7wefij6xxahauck9tgdzs7gv1n66xyvnmpotgfhikofxv1xzm.jpg" caption="Settings &gt; Plugins &gt; Activate" mode="responsive" height="418" width="1920" %}
{% /image %}

---

## Add keys and configure the plugin

{% callout type="warning" title="Before you start" %}
You will need to have completed Onboarding and generated API keys.

[Onboarding](https://developers.yoti.com/age-verification/getting-started)
{% /callout %}

- Open the plugin settings page by going to '**Settings -&gt; Yoti Age Verification**' from the left menu
- Add the SDK ID and API Key
- Set the default age threshold and enable verification methods
- Configure the Notifications webhook

{% image url="https://uploads.developerhub.io/prod/kvAX/neg9aajwwbzjgd7c5unsb3r6vgy318sav7yjrwaiaw6jegqe5lovhn0yklbcrns6.jpg" caption="Settings &gt; Yoti Age Verification" mode="responsive" height="822" width="1920" %}
{% /image %}

- Optionally, customise the plugin inline elements

{% image url="https://uploads.developerhub.io/prod/kvAX/qhwk59oygh2xfrimlrum8w8si6fbuad1e27zwhh3oxw7blx738up70jpe6p0fmsx.jpg" caption="Settings &gt; Yoti Age Verification" mode="responsive" height="780" width="1920" %}
{% /image %}

- Set the AV retention period for logged-in and non logged-in users
- Then, click the **'Save Changes'** button

{% image url="https://uploads.developerhub.io/prod/kvAX/ycdcyfagzbftoeu3q1k0mhnaq5sg5bdc4ru8d54g8tim6qup4xo0qyv2zybsmgxo.jpg" caption="Settings &gt; Yoti Age Verification" mode="responsive" height="462" width="1920" %}
{% /image %}

Congratulations - the setup is complete.

---

## Enable age verification for content

Now that the plugin is installed head to your posts or pages by going to **'Posts -&gt; All Posts'** or **'Pages -&gt; All Pages'**

- For each relevant post/page, set the Age threshold and enable/disable Age verification. Make sure to click the individual **'Save'** buttons after changing the configuration.

{% image url="https://uploads.developerhub.io/prod/kvAX/txwje22z68inzswojy9oe2u2oanqqp4d1dwyfyqtbt7klyvrp8bra9eugja3pkgc.jpg" caption="Posts -&gt; All Posts" mode="responsive" height="682" width="1920" %}
{% /image %}

- It's also possible to use **'Bulk actions'** dropdown to set Age threshold and enable/disable Age verification for multiple posts/pages simultaneously. Click **'Apply'** after selecting the relevant items and desired action.

{% image url="https://uploads.developerhub.io/prod/kvAX/0rrcpgw1077yklvgo7hockolaaqexnjcq0jzw6f8iyeyofw3620utmmm051ghe1k.jpg" caption="Posts -&gt; All Posts" mode="responsive" height="682" width="1920" %}
{% /image %}

---

## End-user flow

The age verification flow will automatically be triggered for restricted content.

1. Whenever a user reaches an Age-restricted post or page, they will be asked to prove their age.

{% image url="https://uploads.developerhub.io/prod/kvAX/pllnn2ffqjco9wj16de2b9br4exyh1ckwjjnk5chy1zvtz7yy7inqidt7vt7cz11.jpg" caption="Age-restricted Post" mode="responsive" height="1272" width="1920" %}
{% /image %}

2. They will be able to confirm their age using any of the allowed methods.

{% image url="https://uploads.developerhub.io/prod/kvAX/ow97iqk6wss6fcztvrxbu0t7iyjtfyegwmirgeco94w2e65m1ktd54ki5ux8yfvg.jpg" caption="Yoti Age Verification" mode="responsive" height="1377" width="1920" %}
{% /image %}

3. The user will get a confirmation once their age is confirmed, and a button will be shown to go back to the website.

{% image url="https://uploads.developerhub.io/prod/kvAX/ohz7a8t9pqs1srw3pax2yyjz2w5t7dlpjvi1g6h9btq31egac1jgdyow37ftbi39.jpg" caption="Age confirmed" mode="responsive" height="916" width="1920" %}
{% /image %}

4. They will then be redirected to the WordPress site and a **thank-you** message will be shown.

{% image url="https://uploads.developerhub.io/prod/kvAX/6mv1ckmex3w8ic7ecgb1ls3pypqfidv4emtkhrz2sy0ls5w24udjjz572oehc7n5.jpg" caption="Age Verification Thank-you" mode="responsive" height="1150" width="1920" %}
{% /image %}

---

## Review the results

Head to your WordPress admin page.

- Open the Users page by going to **'Users -&gt; All Users'**
- The **'Age Verification Status'** for each user will be shown along with the verification details

{% image url="https://uploads.developerhub.io/prod/kvAX/z1n11j6ohgm7wjezbvv9c6pdgdfassmyxr140zhgdk1zflbrywla9b8cbaz24lpf.jpg" caption="Users page" mode="responsive" height="549" width="1920" %}
{% /image %}