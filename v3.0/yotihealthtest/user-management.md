---
type: page
title: User management
listed: false
slug: user-management
description: 
index_title: User management
hidden: 
keywords: 
tags: 
---

Users in the Yoti Health Test application can be managed manually via user management. This page helps you manage these users manually. In order for a user to log in and access a Yoti Health Test application, they must be given access. Access is obtained by being invited to the application by a Yoti Health Test administrator. 

You must have the **Settings** and **User Management** permission to be able to manage users in Yoti Health Test applications.

---

## Add a user

1. Select **Admin** and then **User Management.**
2. **I**n the User browser, click **Add user**.
3. Enter the **Email address.**
4. Select what permissions you want to give to this user (see Permissions below for more details).
5. Click the **Add user** button.

After the user is created, you’ll be brought to a screen where you can view the user in the users table. The user will receive an invitation email that directs them to the create account screen in the Yoti Health Test application. They can use their Yoti app or create a password to get access to the application.

---

## Edit a user

Modifying user information and permissions is easy in User Management. Please note that you won’t be able to edit a user’s email address as this is associated with testing and cannot be changed.

1. Select **Admin** and then **User Management.**
2. Find the user in the user list or search using their full email address.
3. Click the [icon] edit icon. ✏️
1. Make your changes and click **Update user** to finish.

---

## Change a password

Users can easily change their own password via the login screen by selecting **Forgot password.** This will allow a user to submit their email address, which will send a reset password email.

We strongly recommend that all users log in using their Yoti app. This ensures that your users utilise the highest safety and security standards Yoti has to offer.

---

## Disabling a user

You can disable a user’s account to prevent them from using Yoti Health Test.

1. Select **Admin** and then **User Management.**
2. Find the user in the user list or search using their full email address.
3. Click the [icon] **Remove all permissions** icon found under the Permissions column.

---

## Delete a User

If you have a user that no longer needs access to Yoti Health Test, we recommend that you disable their account rather than delete them. Disabling a user's account will prevent the account from being used, but it will also preserve that user's history of activity.

1. Select **Admin** and then **User Management.**
2. Find the user in the user list or search using their full email address.
3. Click the [icon] edit icon.
4. Select **Delete user** button.

---

### Permissions

You won't want every user in your team to have the same level of access to Yoti Health Test. For example, you may want to restrict who can administer Yoti Health Test, or prevent users from uploading test results. In this step, you will learn about the different permissions in Yoti Health Test and set permissions for each of your users.

You can set the following permissions for each user:

{% table %}
| Access Role | Description | 
| ---- | ---- | 
| Collect samples | A user can collect a test sample and capture personal information to link a customer to their sample. | 
| Prepare test plates | A user can allocate test samples to wells in a testing plate, in preparation for testing the samples in a machine. | 
| Run machine and upload results | A user can take an exported data file from a test machine and upload it to the Yoti Health Test application for processing. | 
| Export data and Reporting | A user can view all test data and download test data currently stored on Yoti’s secure servers. | 
| Held results | A user has access to the held results area, where they can manage customer test results currently on hold for review. | 
| User management | A user can manage all user accounts and permissions in their Yoti Health Test application. _(This should only be given to someone who acts as an administrator for your Yoti Health Test application.)_ | 
| Settings | A user can access all the configuration settings for the application. (_This should only be given to someone who acts as an administrator for your Yoti Health Test application.)_ | 
{% /table %}