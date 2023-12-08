---
icon: material/monitor-shimmer
title: "Access the Admin UI"
description: "Learn how to access the administrator interface for Glean and add additional administrators."
lang: en
tags:
    - "administration"
    - "getting started"
authors:
    - "Nathan Catania"
---
![](assets/adminui.en.20231208144201697.webp)

In this section, you will learn how to access the Glean Administrator User Interface (UI) and begin setup for your organization.

## About the Glean Admin UI
The Glean Admin UI ([app.glean.com/admin](https://app.glean.com/admin)) is where you will manage the Glean workspace for your organization, including setting up Single Sign-On (SSO), configuring data sources, and syncing people data.

## Sign In to the Admin Interface

To access the Glean Admin UI, navigate to [https://app.glean.com/admin](https://app.glean.com/admin) in your web browser. If you are not already logged in, you will be prompted to do so. Enter your company email address to log in.

![glean-1700136034954-2x](assets/adminui.en.20231208144201720.webp)

Because we have not configured Single Sign-On (SSO) yet, you will be prompted to check your email for a link to log in. This is called a **Magic Link**. Click the Magic Link in your inbox to log in.

![glean-1700136098518-2x](assets/adminui.en.20231208144201769.webp)

## Add Additional Administrators



When you sign in for the first time, you will be prompted to add additional administrators before proceeding.

![glean-1700386307365-2x](assets/adminui.en.20231208144201801.webp)

There are two types of administrator roles, **Full Admin** and **Setup Admin**:

* A **Full Admin** has full read/write privileges across the admin UI. They can add/remove other admins, manage user permissions, configure data sources, start crawls, and customize the Glean workspace for the organization.
* A **Setup Admin**, has restricted permissions and can only connect and configure data sources and start crawls. This is the perfect role to give to the administrators of any cloud applications you wish to connect to Glean.

See more: Administrator roles.

To proceed, add the emails of any additional users whom you wish to make a Glean administrator, or simply skip to the next step.

!!! warning
    Only select individuals within your organization should be granted Full Admin permissions.

!!! info "Hosting Glean in your own GCP or AWS?"
    You will need to follow the appropriate cloud-prem guide for deploying Glean in GCP or AWS before you can proceed with the rest of this guide.

    * [Deploying Glean in GCP](deploy-gcp.en.md)
    * [Deploying Glean in AWS](deploy-aws.en.md)