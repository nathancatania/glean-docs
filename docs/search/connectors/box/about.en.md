---
icon: material/information
title: "Overview"
description: "The Glean Box connector enables secure and efficient data fetching from your enterprise Box tenant."
sources:
  - https://docs.google.com/document/d/1JKGQbJlkzf-PPpc7k7mxDfKPUVm8bszZ429YUA0HGD4/edit#heading=h.6c3il4soxcwl
---

# Box Connector Overview

## About the Box Connector
The Glean Box connector enables secure and efficient data fetching from your enterprise Box tenant. User permissions are strictly enforced and all data remains securely within your environment.

* Glean requires authentication to the Box instance to fetch relevant information.
* OAuth2 is used to authenticate Glean with your Box account.
    * More information: [OAuth 2.0 (developer.box.com)](https://developer.box.com/guides/authentication/select/#oauth-20){:target="_blank}
* Glean understands all user access permissions and strictly enforces permissions for users at the time of the query. This ensures that users are not able to see results that they do not have access to.
* All data indexed by Glean is stored securely within your Glean tenant. Glean operates a single-tenant architecture where all Glean customers are isolated from each other. No data ever leaves your tenant.


## Integration Features
For Box, Glean indexes the following content and associated permissions:

* Folders
* Files
* Box Notes
* Comments on the files

Glean **does not** currently index:

* Box Web Links
* Custom metadata on files/folders
* Favorites Collections


## API Usage

### Overview

Glean will use the [Box API](https://developer.box.com/reference/){:target="_blank} to ingest all data set up via an enterprise application. This is facilitated via the Glean app in the [Box App Center](https://app.box.com/app-center/glean_search/app/gQSMcDoLbs){:target="_blank"}.

* Glean begins by understanding users of the Box organization and their associated groups.
* Glean crawl folders and associated permissions within each user's Box folders.
* Glean recursively crawls files underneath all folders along with their associated permissions.
* Glean uses webhooks to keep up-to-date with permission changes, folder/file additions and deletions, etc.

Glean performs a monthly full crawl of the content and uses incremental crawls to update existing content and permissions several times every hour.

:octicons-arrow-right-24: More information: [Box API Endpoints](api-endpoints.en.md)

:octicons-arrow-right-24: More information: [Crawling Frequency](../crawling-frequency.en.md#data-refresh-rates)

### Box App Center
As integration between Glean and Box is via the Glean app in the Box App Center, the API calls made are not chargeable by Box (as long as the Glean app is used).

### Rate Limits
The rate at which Glean can crawl your Box documents will depend on the rate limit for the Box API, and will vary from account-to-account.

If you will be indexing a large volume of content from Box with Glean, we recommend getting in touch with your Box Account Team to discuss any applicable API restrictions for your account.


## Setup Prerequisites
A Box admin of the organization is required to set up the enterprise app with the proper permissions for API access to the entire Box corpus.

!!! warning
	Do not attempt to use a co-admin account.
	
	Co-admins cannot access the items of other co-admins, which will cause the crawl to fail.


## Suppressing Box Notifications
The Glean connector connects via the Box API to index data from within your Box environment.

This activity will be correctly identified as `Glean Search` in your Box logs. This activity needs to be considered when [enterprise notifications](https://support.box.com/hc/en-us/articles/360044194073-Manage-Notifications-for-Enterprise-Users) are enabled on a large set of these documents.

Work with your Box representative to [suppress notifications](https://developer.box.com/guides/api-calls/suppress-notifications/) for the [Glean Search](https://cloud.app.box.com/app-center/glean_search/app/gQSMcDoLbs) application. Once enabled, Glean can adjust our API calls to include the suppression directive so that your organization is not overwhelmed with notifications.


## Content Restrictions
Glean supports multiple methods to restrict the Box content indexed by Glean.

:octicons-arrow-right-24: More information: [Restricting Content for Box](restrict.en.md)