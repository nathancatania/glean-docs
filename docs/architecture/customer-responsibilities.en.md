---
icon: octicons/code-of-conduct-24
title: "Customer Responsibilities for Managing Glean"
description: ""
sources:
    - "[External] Customer shared responsibility for managing Glean"
---

As a Glean customer and administrator for your company, you are responsible for the following security best practices when managing your Glean tenant.

## Employee Access Controls

1. As a Glean customer, you must ensure that the Single Sign-On (SSO) conditional access policy configured in Glean meets the security requirements of your organization. This includes the application of additional security controls like Multi-Factor Authentication (MFA) or Trusted Locations (i.e. IP Greenlisting).

2. As a Glean customer, you must ensure only users who are intended to use Glean are added to the SSO provider that Glean is configured with.

3. As a Glean customer, you must ensure prompt removal of terminated employees/contractors from the SSO provider configured for Glean, so they lose Glean access promptly. This process is typically automated on the Glean side when an employee is removed or disabled in your directory through OIDC or SCIM Provisioning.

4. As a Glean customer, you should have a clear policy for who can be assigned an administrator role within your Glean tenant, and should utilize Glean's Role-Based Access Controls (RBAC) to ensure that different admins have permissions only for the parts of the Glean workspace setup they need to access and manage.

5. If your Glean users are intended to be coming from specific IP ranges (e.g. you are using a VPN), then the customer should ensure that an IP green list is configured in Glean. As a Glean customer, it is your responsibility to ensure that this list of IP addresses/IP ranges is kept up-to-date.


## Connector Integrations

1. As a Glean customer, you are responsible for rotating the credentials of the datasources that Glean uses to connect to them. You must ensure that Glean is provided with any rotated credentials (API key, authorization token, client secret, etc) in a timely manner so that crawling and indexing of your are not disrupted.

2. Wherever feasible, you should use service users/service accounts when setting up the integration between Glean and your source applications. Configuring integrations that leverage a specific employee's access credentials should be avoided so that the integrations continue working if the employee leaves the company.


## Cloud-prem Considerations
If you are hosting your Glean tenant within your own GCP or AWS environment, then there are additional security considerations and responsibilities to be aware of.

:octicons-arrow-right-24: More information: [Customer Responsibilities for Cloud-Prem](){:target="_blank"}.