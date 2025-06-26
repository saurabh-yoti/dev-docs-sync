---
type: page
title: Set up
listed: true
slug: setup
description: 
index_title: Set up
hidden: 
keywords: 
tags: 
---

Once you've set up your organisation account you’re ready to start integrating with Health portal.

{% html %}
<div class="alert-BYS">
   <div class="alert-title" id="BYS">
      Before you start
   </div>
   <div class="alert-text" >
Please contact us to get you onboard.  </div>
   <div class="alert-links"> 
      <a  target="_self" href="mailto:clientsupport@yoti.com"> Contact us </a>
   </div>
</div>
{% /html %}

The following steps are:

1. Register your email
2. Add users
3. Organisation details
4. Machine management

As the admin of the system you should receive an email asking you to sign up to the portal. You can sign up to the portal with two options:

- Sign up with Yoti.
- Email address and password

### Sign up with Yoti

Yoti is available in the the play store and the app store.

1. Download the Yoti app.
2. Add the email address you would like to use to login to the system to create your account.

{% badge type="info" text="Hint" /%} You do not need to add a document to your Yoti to use this service.

{% video %}
{% /video %}

After you have downloaded the app press the SIGN UP WITH YOTI button and scan the QR code with the Yoti app.

{% badge type="warning" text="Help" /%} If you need any help please email [help@yoti.com](mailto:help@yoti.com).

### Email and password

If you do not wish to set up your account with Yoti you can also use username and password.

- Enter the email address you would like to use to login to the system to create your account.
- Create a secure password.
- Tick the terms and conditions
- Press "**CREATE YOUR ACCOUNT".**

{% image url="https://res.cloudinary.com/developerhub/image/upload/v1615818907/v2_2762/rlw3lbeqhykjgyiprbgx.png" caption="Create your account" mode="600" height="1458" width="930" %}
{% /image %}

- After this you will need to check your emails for a verification link. 

{% image url="https://res.cloudinary.com/developerhub/image/upload/v1615818969/v2_2762/drub0ezl19xqx9mqa6jf.png" caption="Email verification" mode="600" height="610" width="1062" %}
{% /image %}

Click the verification link in your inbox to open the portal. Here you will be asked to login to the system. 

{% badge type="info" text="Hint" /%} If you do not get this email please check your JUNK email. If you still cant see the email please email [clientsupport@yoti.com](clientsupport@yoti.com)

---

### Login

Type the same email address and password in and you be all logged in!

{% image url="https://res.cloudinary.com/developerhub/image/upload/v1615819219/v2_2762/czpmv8zfbap1fvrntrdk.png" caption="Login" mode="600" height="1210" width="914" %}
{% /image %}

{% html %}
<div class="alert-GTK">
    <div class="alert-title" id="GTK">
        Good to know
    </div>
    <div class="alert-text">
Users can easily change their own password via the login screen by selecting Forgot password. This will allow a user to submit their email address, which will send a reset password email.

We strongly recommend that all users log in using their Yoti app. This ensures that your users utilise the highest safety and security standards Yoti has to offer.
    </div>
    <div class="alert-links"> 
         <a href="https://developers.yoti.com/health-test/setup#add-a-user">Add a user</a>
   </div>
</div>
{% /html %}

If you have multi organisations set up with us you will be able to toggle between them:

{% image url="https://res.cloudinary.com/developerhub/image/upload/v1616706357/v2_2762/gzc9dieg76dzwjgok44c.png" caption="Home &gt; Org options" mode="responsive" height="1570" width="2880" %}
{% /image %}

---

## User management

### Add a user

Once you are in, the next step would be to add your users. Head over to the hamburger menu and press ADMIN. 

{% image url="https://res.cloudinary.com/developerhub/image/upload/v1615824096/v2_2762/vqsqbkkbq5nw6jnxemio.png" caption="Hamburger menu &gt; Admin" mode="responsive" height="224" width="428" %}
{% /image %}

- Click **User management.**

{% image url="https://res.cloudinary.com/developerhub/image/upload/v1615824128/v2_2762/st4t8mhqviw3mwgqxigs.png" caption="User management &gt; Add a user" mode="responsive" height="213" width="1636" %}
{% /image %}

- Click **Add user**
- Enter the users email address. 
- Select the permissions you want to give the user. 

{% image url="https://res.cloudinary.com/developerhub/image/upload/v1615824168/v2_2762/ne1s6mncecwqy6bnbnap.png" caption="User management &gt; Add user" mode="responsive" height="689" width="338" %}
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

### Edit a user

Modifying user information and permissions is easy in User Management.

{% badge type="info" text="Hint" /%} You won’t be able to edit a user’s email address as this is associated with testing and cannot be changed.

- Select **Admin** and then **User Management.**
- Find the user in the user list or search using their full email address.
- Click the ✏️ edit icon.
- Make your changes and click **Update user** to finish.

{% image url="https://res.cloudinary.com/developerhub/image/upload/v1615824280/v2_2762/afi2vdah1nyaulbf43i7.png" caption="User management &gt; Edit" mode="responsive" height="211" width="1633" %}
{% /image %}

### Disable a user

You can disable a user’s account to prevent them from using the portal:

1. Select **Admin** and then **User Management.**
2. Find the user in the user list or search using their full email address.
3. Click the 🚫 **Remove all permissions** icon found under the Permissions column.

{% image url="https://res.cloudinary.com/developerhub/image/upload/v1615824440/v2_2762/nuaexujwmz5ggb0sre4i.png" caption="User management &gt; Disable" mode="responsive" height="216" width="1643" %}
{% /image %}

### Delete a user

If you have a user that no longer needs access to the portal, we recommend that you disable their account rather than delete them. Disabling a user's account will prevent the account from being used, but it will also preserve that user's history of activity.

1. Select **Admin** and then **User Management.**
2. Find the user in the user list or search using their full email address.
3. Click the ✏️ edit icon.
4. Select **Delete user** button.

{% image url="https://res.cloudinary.com/developerhub/image/upload/v1615824558/v2_2762/f0hdbceqqw3h1wl8nvz5.png" caption="User management &gt; Click user &gt; Delete User" mode="responsive" height="706" width="334" %}
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