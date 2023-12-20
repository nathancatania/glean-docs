---
icon: material/information
title: "GCP Service Account with Owner Role"
description: "Glean provides a universal enterprise search tool that allows users to search their data scattered across multiple applications (e.g. Gdrive, Slack, Salesforce, SharePoint, Zendesk, etc.) from a single interface."
sources:
    - https://docs.google.com/document/d/1bvLE0u-L-OnlgFwpfGpY_BXdq9ZwIgE1jaLMs8Xjmmw/edit?usp=sharing
---

As part of the process for deploying Glean within your organization's own Google Cloud Platform (GCP) environment, Glean mandates the creation of a Service Account with Owner role permissions attached to it.

This document discusses the purpose of the service account, how Glean leverages it, and how your organization can manage it securely.

## About the GCP Service Account with Owner Role
The GCP service account with the Owner role allows those with access the ability to view and manage any of the infrastructure or data within the GCP project in which Glean is hosted.

As part of the build process for your tenant, Glean requires that a service account with owner role priviledges be created. This account is used by Glean's automated build pipelines to deploy your Glean tenant within the designated project.

Glean is granted access to the service account through a JSON key that is uploaded securely via the Glean UI. 

!!! tip
    A service account that is generated with an owner role for a specific project in Google Cloud Platform (GCP) is limited to the resources and services within that specific project. It does not have permissions to access or modify resources outside of that project, even if it's within the same GCP tenant.

    The permissions of a service account are defined by the roles that are granted to it. The owner role grants full access to all resources in the project where it is assigned, but it does not extend to other projects in the GCP tenant.

!!! warning
    Glean cannot deploy your tenant without the owner role, as it allows our build system to create all resources required by the Glean platform within the project; including instances, storage, databases, workflows, dashboards, networking, and security configuration.

    It is not possible to create these resources manually yourself: Glean leverages Infrastructre as Code (IaC) to ensure the integrity and validity of our deploys. Manually creating resources would not only be time-consuming and prone to human error, but it would also bypass our automated deployment and configuration processes. These processes are designed to ensure consistency, reliability, and security across all deployments of the Glean platform.


## Controlling Access to the Service Account with Owner Role