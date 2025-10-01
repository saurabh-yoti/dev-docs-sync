---
type: page
title: User management
listed: true
slug: user-management
description: 
index_title: User management
hidden: 
keywords: 
tags: 
---

Once you are in, the next step would be to add your users. Head over to the hamburger menu and press ADMIN.

{% image url="https://image-archive.developerhub.io/image/upload/v2_2762/vqsqbkkbq5nw6jnxemio/1615824096.png" caption="Hamburger menu &gt; Admin" mode="responsive" height="224" width="428" %}
{% /image %}

- Click **User management.**

{% image url="https://image-archive.developerhub.io/image/upload/v2_2762/st4t8mhqviw3mwgqxigs/1615824128.png" caption="User management &gt; Add a user" mode="responsive" height="213" width="1636" %}
{% /image %}

- Click **Add user**
- Enter the users email address. 
- Select the permissions you want to give the user. 

{% image url="https://image-archive.developerhub.io/image/upload/v2_2762/ne1s6mncecwqy6bnbnap/1615824168.png" caption="User management &gt; Add user" mode="responsive" height="689" width="338" %}
{% /image %}

The different levels of access are described below:

{% table %}
| Access Role | Description | 
| ---- | ---- | 
| Customer data | A user can upload a csv with customer data that have pre-registered to be tested. | 
| Collect samples | A user can collect a test sample and capture personal information to link a customer to their sample. | 
| Prepare test plates | A user can allocate test samples to wells in a testing plate, in preparation for testing the samples in a machine. | 
| Run machine and upload results | A user can take an exported data file from a test machine and upload it to the portal for processing. | 
| Reporting | A user can view all test data and download test data currently stored on Yoti’s secure servers. | 
| Held results | A user has access to the held results area, where they can manage customer test results currently on hold for review. | 
| User management | A user can manage all user accounts and permissions in the portal. _(This should only be given to someone who acts as an administrator for your portal)_ | 
| Settings | A user can access all the configuration settings for the application. (_This should only be given to someone who acts as an administrator for your portal)_ | 
{% /table %}

After the user is created, you’ll be brought to a screen where you can view the user in the users table. The user will receive an invitation email that directs them to the create account screen in the portal. They can use their Yoti app or create a password to get access to the application.

---

## Edit a user

Modifying user information and permissions is easy in User Management.

{% badge type="info" text="Hint" /%} You won’t be able to edit a user’s email address as this is associated with testing and cannot be changed.

- Select **Admin** and then **User Management.**
- Find the user in the user list or search using their full email address.
- Click the ✏️ edit icon.
- Make your changes and click **Update user** to finish.

{% image url="https://image-archive.developerhub.io/image/upload/v2_2762/afi2vdah1nyaulbf43i7/1615824280.png" caption="User management &gt; Edit" mode="responsive" height="211" width="1633" %}
{% /image %}

---

## Disable a user

You can disable a user’s account to prevent them from using the portal:

1. Select **Admin** and then **User Management.**
2. Find the user in the user list or search using their full email address.
3. Click the 🚫 **Remove all permissions** icon found under the Permissions column.

{% image url="https://image-archive.developerhub.io/image/upload/v2_2762/nuaexujwmz5ggb0sre4i/1615824440.png" caption="User management &gt; Disable" mode="responsive" height="216" width="1643" %}
{% /image %}

---

## Delete a user

If you have a user that no longer needs access to the portal, we recommend that you disable their account rather than delete them. Disabling a user's account will prevent the account from being used, but it will also preserve that user's history of activity.

1. Select **Admin** and then **User Management.**
2. Find the user in the user list or search using their full email address.
3. Click the ✏️ edit icon.
4. Select **Delete user** button.

{% image url="https://image-archive.developerhub.io/image/upload/v2_2762/f0hdbceqqw3h1wl8nvz5/1615824558.png" caption="User management &gt; Click user &gt; Delete User" mode="responsive" height="706" width="334" %}
{% /image %}

{% html %}
<div class="alert-GTK">
    <div class="alert-title" id="GTK">
        Good to know
    </div>
    <div class="alert-text">
       All tests associated with a deleted user will no longer show who did the collecting/testing, and will instead show an anonymous user ID number.

Deleted users can still log in, after which they will be informed that their access has been removed.

All this ensures that test data is not affected by actions made in user management.
    </div>
    <div class="alert-links"> 

   </div>
</div>
{% /html %}