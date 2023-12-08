---
icon: material/hammer-wrench
title: "Glean Deployment Options"
description: "Glean is a SaaS solution and all tenants are hosted by Glean by default, however Glean also provides options for our customer's to self-host Glean within their own GCP or AWS environments."
lang: en
tags:
    - "getting started"
    - "administration"
    - "saas"
    - "cloud-prem"
    - "GCP"
    - "AWS"
    - "deployment"
authors:
    - "Nathan Catania"
sources:
    - https://docs.google.com/document/d/1WvmtYulF7gMMjyCBTsaRdxVgkY694PcBIWFnRR2kFLs/edit
---

![](assets/deploy-options.en.20231208144202742.webp)

## About Glean Deployments
Glean is a SaaS solution where all customer tenants are hosted by Glean by default as part of our SaaS offering.

Glean also provides options for our customers to self-host their Glean tenant within their own GCP or AWS environment.


## Glean Hosted
By default, Glean builds each customer environment from scratch to ensure resiliency and isolation from all other customers.

This provides several advantages for you:

1. Simplified setup process.
2. No requirement for engineering resources to manage the system.
3. Full auto-scaling as the corpus and users grow.
4. Rely on Glean's security controls and guarantees to protect your data.
5. Simpler licensing and pricing model. Lower cost due to amortization of maintenance cost on Glean's side. Pay a fixed fee per active user per month.

In terms of access to your tenant:

* No employee at Glean retains access to any customer data.
* Glean only receives sanitized logs (all PII removed) and metrics to support your instance - all actual data that Glean has indexed remains inside your isolated tenant.
* To debug production issues or provide support where access to sensitive logs/components is required, our engineers are required to:
    * Justify access.
    * Obtain approval from your organization.
    * Obtain approval from the Glean security team.
    * All granted access is audited and time-bound for 1-hour.


## Cloud-prem (GCP/AWS) Hosted
In the Cloud-prem model, your Glean tenant is deployed and managed by Glean within your own cloud environment (i.e. GCP, AWS). 

This has a few advantages:
management,
1. **Data Security and Control:** Know exactly where your data is and the fact that the data never leaves your environment. Control GCP/AWS IAM policies yourself and retain direct access to logs.

2. **Retire Spend Against Your Commit:** Retire the costs of hosting Glean against your spend commitment with GCP or AWS.

3. **Lower Glean Pricing:** Receive a discount on your Glean subscription cost as we no longer need to host the infrastructure for your tenant ourselves.

Unlike traditional "self-hosted" options, with the cloud-prem model Glean still fully manages your deployment; including upgrades, patching, and monitoring - the same as the Glean-hosted option.

This is possible, without having access to any of your company data within your tenant, due to restricted IAM controls that are put in place during the build of your tenant. These controls restrict Glean access to only project management with no access to underlying data stored in the project.

!!! warning
    Deliberately restricting or blocking Glean access to your tenant will void Glean's Service and Support SLAs, and may impact the ability for our support teams to assist you when troubleshooting issues.
    
    This also prevents Glean from rolling updates to your tenant (including security fixes), which may put it at risk.










