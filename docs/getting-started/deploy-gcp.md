---
icon: material/google-cloud
title: "Deploying Glean in GCP"
description: "Your Glean instance can be deployed within your own GCP environment to allow you to retire compute costs against your committed spend."
draft: true
authors:
    - "Nathan Catania"
sources:
    - https://docs.google.com/document/d/1HEGcjUZjhrSamFuSxsbHOyGroU0ut7TmG5sKAWEfrBg/edit
    - https://docs.google.com/spreadsheets/d/1THwN43trfMqwUggrslOKDxLrB3uDIJ536MnIQzwZCV8/edit#gid=921403900
---

## About Cloud-prem GCP

Glean provides our customers the ability to deploy Glean software inside of their own GCP Project. This deployment requires your GCP admin to create a new GCP project, associate a **billing account** to it, enable applicable APIs, and request the required quotas from GCP.

After completing the above, Glean's systems will automatically build and deploy the required compute, workflows, and software into your GCP project.

At this stage, Glean will advise you that your tenant is ready; allowing your admins to proceed with the setup process in our [Get Started guide](welcome.md) by connecting to an SSO provider and relevant data sources.

This document will cover the steps required by your GCP admins to prepare a GCP project that is ready for your Glean build.

## 1. Create the GCP Project
1. Go to the [Manage resources](https://console.cloud.google.com/cloud-resource-manager) page in the GCP console and click Create Project.

2. In the New Project window that appears, add a project name, organization, and location.
    * For project name, the preferred format is `glean-{customer name}` or `glean-{customer name}-{prod/sandbox}`, eg: `glean-company` or `glean-company-prod`

3. Make sure your project is created under the same organization as your Google Workplace account, and **not** “No Organization”.

    !!! danger
        Glean is not able to proceed with the build if the project is created under "No Organization". If you are unsure of how to resolve this, please contact your GCP rep or GCP support.

4. Save the Project ID (which is directly below the Project name) and Project Number.

5. Click **Create**.

6. Notify Glean of the following information:

    a. Project name, eg `glean-company` -> This was set in Step 2 above.
    
    b. Project ID, eg `glean-company` -> This was saved in Step 4 above.
    
    c. Project number, eg `715000000000` -> This was saved in Step 4 above.


## 2. Configure Billing
1. Go to [Billing](https://console.cloud.google.com/billing/linkedaccount) in the GCP console.

2. Click **Link a billing account** to set up billing for this project.
   
    !!! warning
        Ensure that the billing account has a corporate credit card attached to it. Using the “free trial billing tier” will not work.


## 3. Enable APIs
Glean requires that the following GCP APIs are enabled for the deploy to succeed. Substitute your Project ID to the end of the URL for each API below to enable the API on the project.

| API Name                                                     | URL                                                          |
| ------------------------------------------------------------ | ------------------------------------------------------------ |
| Cloud Resource Manager API (cloudresourcemanager.googleapis.com) | `https://console.cloud.google.com/apis/api/cloudresourcemanager.googleapis.com/overview?project=[PROJECT_ID]` |
| Service Usage API (serviceusage.googleapis.com)              | `https://console.developers.google.com/apis/api/serviceusage.googleapis.com/overview?project=[PROJECT_ID]` |
| Compute Engine API (compute.googleapis.com)                  | `https://console.developers.google.com/apis/api/compute.googleapis.com/overview?project=[PROJECT_ID]` |
| Cloud SQL Admin API (sqladmin.googleapis.com)                | `https://console.developers.google.com/apis/api/sqladmin.googleapis.com/overview?project=[PROJECT_ID]` |



## 4. Request Quota Changes

Search for `[Quotas]` in the search box of the GCP Console and navigate to **All Quotas**, under IAM & Admin.

For each of the quotas in the table below, request a quota change by completing the following:

1. Click on the required quota.
2. Select **Edit Quotas**
3. Enter the value specified by Glean for the quota.
4. Click **Submit Request**.

!!! info
    Please note that some quota requests will require filing a ticket with GCP support. Response time is typically within 2 days.

=== "Large (>2500 employees)"
    {{ read_excel("../assets/tables/gcp-quota-details.xlsx", engine="openpyxl", na_filter=False, skiprows=[0], sheet_name="Large Deployment Quota") }}

=== "Medium (<2500 employees)"
    {{ read_excel("../assets/tables/gcp-quota-details.xlsx", engine="openpyxl", na_filter=False, skiprows=[0], sheet_name="Medium Deployment Quota") }}

=== "Small (test/sandbox)"
    {{ read_excel("../assets/tables/gcp-quota-details.xlsx", engine="openpyxl", na_filter=False, skiprows=[0], sheet_name="Small Deployment Quota") }}

## 5. Create a Service Account
The service account is used to allow Glean's systems to access the project and perform the build. You will create the service account and provide Glean with the private JSON key required to use it.

1. Go to the [Service Accounts](https://console.cloud.google.com/iam-admin/serviceaccounts) page in the GCP console and click Select a Project.

2. Click **Create Service Account**. Enter the service account name (`glean-admin`), ID, and description (optional), then click **Create**.

3. Click the **Select a role** dropdown to make your service account an **Owner** of the project. Click **Continue**.

4. Ignore the **Grant users access to this service account** option. It is not required.

5. Click **Create Key**. In the panel that appears, select the key type **JSON** then **Create**. This will save a private JSON key to your computer.


## 6. Upload the Service Account Key to the Glean Admin UI
1. If you haven't already, follow the instructions from the [Access the Admin UI](adminui.md){:target="_blank} section of the Getting Started guide.
    * Browse to [https://app.glean.com/admin](https://app.glean.com/admin)
    * Enter your email to receive a link via email to sign in.

2. On the page titled Create a Google Cloud Platform project, click the box under Step 2 to upload the private JSON key to Glean.

3. Click **Save**. Glean will now use the JSON key to validate that all of the steps above have been performed correctly.

!!! success
    If the save is successful, your Glean tenant is ready to be built. Contact your Glean contact to proceed.

!!! failure
    If the save fails, you will be presented with a red error message detailing the issues to correct. The key must save correctly before the build of your Glean tenant can proceed.


## FAQ

!!! quote "I don't want to provide Glean with a service account. Can I build everything myself?"
No. Glean utilizes Infrastructure as Code (IaC) and as such, all of our build systems are automated. This ensures ensures consistency, reliability, and security in our deployments.

Providing Glean with a service account allows us to manage these processes effectively. Attempting to build everything yourself would not only be time-consuming but could also lead to potential errors or security risks.


!!! quote "Can I revoke/delete the service account created and associated JSON key after the build is complete?"
Yes. As part of the build, Glean automatically creates a maintenance service account that is used by our systems to automatically manage, update, and patch your environment. The original JSON key and associated account that you provided Glean can be revoked.

!!! quote "I don't want Glean to be able to access the completed build at all for security reasons. Can I revoke the maintenance account as well?"
Technically yes, but Glean **strongly recommends that you leave the maintenance account enabled.**

**Delibrately restricting or blocking Glean's access to your tenant will void Glean's Service and Support SLAs, and may impact our ability for our support teams to assist you when troubleshooting issues.**

This also prevents Glean from rolling updates to your tenant (including security fixes), which may put it at risk.

It is important to remember that Glean is NOT a self-hosted service, and is still cloud-managed; hence we need appropriate access to do so.