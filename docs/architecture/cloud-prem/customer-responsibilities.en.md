---
icon: octicons/code-of-conduct-24
title: "Customer Responsibilities for Cloud-Prem"
description: ""
sources:
    - "[External] Customer shared responsibility for managing Glean"
---

Where the Glean instance is hosted in a project in your organization's own GCP or AWS environment, there are additional requirements that must be considered.

!!! info
    The below responsibilities only apply if your Glean instance is hosted in your organization's own GCP or AWS environment. If you are using Glean SaaS (that is, Glean is hosting your tenant), the below considerations do not apply.

## Administrator Access Control

### Organization Owners
You must ensure that the set of cloud platform (GCP or AWS) organization level owners is strictly controlled, and these owners have secure authentication requirements (MFA etc).

You should assume that organization owners and other organization level individuals with privileged IAM roles (SQL admin, Kubernetes admin, AdministratorAccess, PowerUserAccess, etc) will have access to the stored contents in Glean's cloud project when deployed in your cloud environment, whether it's hosted on GCP or AWS.

### IAM Roles with Project Access
You must should ensure that the group of employees with Identity and Access Management (IAM) access to Glean's cloud project, whether on GCP or AWS, is strictly controlled, and they all have secure authentication requirements (MFA etc).

You should assume that the admins of Glean's cloud project, with privileged IAM roles (such as Owner, Editor, Viewer, SQL admin, Kubernetes admin, AdministratorAccess, PowerUserAccess, ReadOnlyAccess, etc), will have the ability to view the stored contents in Glean's project on either GCP or AWS if they attempt to do so.

Typically, only IT admins with a level of access comparable to a Google Workspace admin or AWS account root user should be added as admins to Glean’s cloud project.


## Access Constraints
Once Glean's cloud project is established, whether on GCP or AWS, the you should activate the organization level constraint that restricts sharing within the domain for the project.

This can be achieved by setting up appropriate IAM policies and resource-based policies on AWS, or enabling the [Domain restricted sharing](https://cloud.google.com/resource-manager/docs/organization-policy/org-policy-constraints){:target="_blank"} org-level constraint on GCP.

You must not alter the default for any other organization level constraint or equivalent settings on either GCP or AWS for the project without first consulting with Glean Support.

## Glean Access

You may choose to revoke Glean's access to the debug service account after the system is in steady state, however you must then the customer must have a process for the prompt enabling/disabling of the said service account so that the Glean can investigate and resolve production issues rapidly.

!!! info
    As all Glean deployments are cloud-managed by Glean regardless of where they are deployed, Glean does not recommend that customer's revoke access to the debug service account unless absolutely necessary.

!!! warning
    If Glean is unable to act to resolve a service unavailability event or investigate an issue requested by the customer, Glean cannot offer or enforce any customer-committed SLAs.
    
    It is in the best interest of your organization to have an always-available staff and process for providing the debug access to Glean at a moments notice, or alternatively, to leave the service account enabled.



## Service Modifications
!!! danger
    Modifying the services within the Glean project may cause service disruption and will void any SLAs in place with Glean.

You **must not** make any modifications to the GCP or AWS project without consulting with Glean Support. For instance, incompatible modifications to the firewall rules or IAM permissions of GCP/AWS components like SQL, Cloud Storage etc in the project could lead to service disruption.

Additionally, you **must not** run other services in the project without approval from Glean Support.

## Logging
Glean encourages our customers to export or stream the application and cloud audit logs for their Glean deployment to their SIEM, and for custom alerts/anomoly detection to be configured.


## Security Services
You may optionally enable certain security services within your Glean project to enhance the overall security of the system. For example, [Intrusion Detection System](https://cloud.google.com/intrusion-detection-system){:target="_blank"} and/or [Cloud Armor](https://cloud.google.com/armor){:target="_blank"} in GCP.

Glean recommends consulting with Glean Support or your Glean Customer Success Manager to ascertain which services have been validated by Glean.

