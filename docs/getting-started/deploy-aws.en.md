---
icon: material/aws
title: Deploying Glean in AWS
description: Your Glean instance can be deployed within your own AWS environment to allow you to retire compute costs against your committed spend.
lang: en
authors:
  - Nathan Catania
---
![](assets/deploy-aws.en.20231128230345835.webp)
## About Cloud-prem AWS

Glean provides our customers the ability to deploy Glean software inside of their own AWS environment. This deployment requires your AWS admin to create a new AWS project, associate a **billing account** to it, enable applicable APIs, and request the required quotas from AWS.

After completing the above, Glean's systems will automatically build and deploy the required compute, workflows, and software into your AWS project.

At this stage, Glean will advise you that your tenant is ready; allowing your admins to proceed with the setup process in our [Get Started guide](welcome.en.md) by connecting to an SSO provider and relevant data sources.

This document will cover the steps required by your AWS admins to prepare a AWS project that is ready for your Glean build.











