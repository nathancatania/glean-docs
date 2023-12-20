---
icon: material/api
title: "API Endpoints"
description: "The Glean M365 connectors enable secure and efficient data fetching from your M365 tenant."
---

Glean will use the standard Graph API v1.0 and [Sharepoint REST API](https://docs.microsoft.com/en-us/sharepoint/dev/sp-add-ins/get-to-know-the-sharepoint-rest-service?tabs=csom){:target="_blank} to ingest data. We use application permissions with admin-granted access.

Glean uses the recommended [best practices](https://docs.microsoft.com/en-us/onedrive/developer/rest-api/concepts/scan-guidance?view=odsp-graph-online){:target="_blank} strategy provided by Microsoft to both crawl and record incremental changes for all documents.

## Authentication Endpoints

| Endpoint | Use Case | Documentation | Product |
|---|---|---|---|
| Token request (Graph API)<br>`https://login.microsoftonline.com/{tenant}/oauth2/v2.0/token` | Obtain and refresh an access token to interact with the Graph API using OAuth 2.0. | [Token request - Microsoft Graph API](https://learn.microsoft.com/en-us/graph/auth-v2-service?tabs=http#token-request){:target="_blank"} | All |
| Token request (SharePoint REST API)<br>`https://accounts.accesscontrol.windows.net/<tenant_id>/tokens/OAuth/2` | Obtain and refresh an access token to interact with the SharePoint REST API using OAuth 2.0. | [Get to know the SharePoint REST service - SharePoint REST APIs](https://learn.microsoft.com/en-us/sharepoint/dev/sp-add-ins/get-to-know-the-sharepoint-rest-service?tabs=csom){:target="_blank"} | SharePoint, OneDrive |


## Identity Endpoints

| Endpoint | Permissions | Use Case | Documentation | Product |
|---|---|---|---|---|
| List users<br>`https://graph.microsoft.com/v1.0/users` | User.Read.All<br>Directory.Read.All | List all the users within the tenant. | [List users - Microsoft Graph API](https://learn.microsoft.com/en-us/graph/api/user-list?view=graph-rest-1.0&tabs=http){:target="_blank"} | All |
| List groups<br>`https://graph.microsoft.com/v1.0/groups` | Group.Read.All<br>Directory.Read.All | List all the groups within the tenant. | [List groups - Microsoft Graph API](https://learn.microsoft.com/en-us/graph/api/group-list?view=graph-rest-1.0&tabs=http){:target="_blank"} | All |
| List group members<br>`https://graph.microsoft.com/v1.0/groups/<group_id>/members` | Group.Read.All<br>Directory.Read.All | List all the groups within the tenant. | [List group members - Microsoft Graph API](https://learn.microsoft.com/en-us/graph/api/group-list-members?view=graph-rest-1.0&tabs=http){:target="_blank"} | All |
| Get profilePhoto<br>`https://graph.microsoft.com/v1.0/users/<user_id>/photo/$value` | GroupMember.Read.All<br>Directory.Read.All  | Get the members of a group. | [Get profilePhoto - Microsoft Graph API](https://learn.microsoft.com/en-us/graph/api/profilephoto-get?view=graph-rest-1.0){:target="_blank"} | Azure AD / Entra ID |
| Get site groups<br>`https://<site_domain>.sharepoint.com/sites/<subsite_url>/_api/web/SiteGroups?$expand=Users` | SharePoint REST API Permissions  | Get the default site groups and associated user memberships for a given site.  | [Determine SharePoint REST service endpoint URIs - SharePoint REST API](https://learn.microsoft.com/en-us/sharepoint/dev/sp-add-ins/determine-sharepoint-rest-service-endpoint-uris?tabs=csom){:target="_blank"} | SharePoint, OneDrive |

## Content Endpoints

### Sites
!!! info
    Sites are required to be crawled for both SharePoint site pages and site metadata needed for associated Document Library crawls.

| Endpoint | Permissions | Use Case | Documentation | Product |
|---|---|---|---|---|
| List sites<br>`https://graph.microsoft.com/v1.0/sites/delta` | Sites.Read.All | List all site collections within the tenant. | [List sites - Microsoft Graph API](https://learn.microsoft.com/en-us/graph/api/site-list?view=graph-rest-1.0){:target="_blank"} | SharePoint, OneDrive |
| List subsites<br>`https://graph.microsoft.com/v1.0/sites/<id>/sites` | Sites.Read.All | List all the subsites within a site or subsite. | [List subsites - Microsoft Graph API](https://learn.microsoft.com/en-us/graph/api/site-list-subsites?view=graph-rest-1.0&tabs=http){:target="_blank"} | SharePoint, OneDrive |
| List lists<br>`https://graph.microsoft.com/v1.0/sites/<site_id>/lists` | Sites.Read.All | List all the lists within the site. | [List lists - Microsoft Graph API](https://learn.microsoft.com/en-us/graph/api/list-list?view=graph-rest-1.0&tabs=http){:target="_blank"} | SharePoint, OneDrive |
| List columns<br>`https://graph.microsoft.com/v1.0/sites/<id>/sites/<id>/columns` | Sites.Read.All | List all columns within the site (attributes of site). | [List columns - Microsoft Graph API](https://learn.microsoft.com/en-us/graph/api/site-list-columns?view=graph-rest-1.0&tabs=http){:target="_blank"} | SharePoint, OneDrive |
| List items delta<br>`https://graph.microsoft.com/v1.0/sites/<id>/sites/ <id>/lists/ <id>/item /delta` | Sites.Read.All | List all items from delta endpoint (metadata). | [List item delta - Microsoft Graph API](https://learn.microsoft.com/en-us/graph/api/listitem-delta?view=graph-rest-beta&tabs=http){:target="_blank"} | SharePoint, OneDrive |
| Get site list items<br>`https://<site_domain>.sharepoint.com/sites/<subsite_url>/_api/web/lists('<list_id>')/item` | SharePoint REST API Permissions  | Get the items within a list for a site.<br>SharePoint REST API is used as some content for classic sites is not available via Graph API. | [Determine SharePoint REST service endpoint URIs - SharePoint REST API](https://learn.microsoft.com/en-us/sharepoint/dev/sp-add-ins/determine-sharepoint-rest-service-endpoint-uris?tabs=csom){:target="_blank"} | SharePoint, OneDrive |
| Get site item permissions<br>`https://<site_domain>.sharepoint.com/sites/<subsite_url>/_api/web/lists('<list_id>')/items('<item_id>'/roleassignments` | SharePoint REST API Permissions  | Get the permissions for an item on the site.<br>Sharepoint REST API is required for site pages / web components, as Graph API only exposes permissions for Document Library items. | [Determine SharePoint REST service endpoint URIs - SharePoint REST API](https://learn.microsoft.com/en-us/sharepoint/dev/sp-add-ins/determine-sharepoint-rest-service-endpoint-uris?tabs=csom){:target="_blank"} | SharePoint, OneDrive |
| Get page content<br>`https://<site_domain>.sharepoint.com/sites/<subsite_url>/_api/web/GetFileById('<id>')/GetLimitedWebPartManager(scope=1)/ExportWebPart` | SharePoint REST API Permissions  | Get the web parts on a particular page (e.g. blocks of content within text boxes, titles, etc.) | [Determine SharePoint REST service endpoint URIs - SharePoint REST API](https://learn.microsoft.com/en-us/sharepoint/dev/sp-add-ins/determine-sharepoint-rest-service-endpoint-uris?tabs=csom){:target="_blank"} | SharePoint, OneDrive |


### Drives
Drives include both OneDrive for Business (user drives) and Document Libraries on Sharepoint Sites.

| Endpoint | Permissions | Use Case | Documentation | Product |
|---|---|---|---|---|
| List drives<br>`https://graph.microsoft.com/v1.0/sites/<site_id>/drives` | Files.Read.All | List all the drives within a given site. | [List drives - Microsoft Graph API](https://learn.microsoft.com/en-us/graph/api/drive-list?view=graph-rest-1.0&tabs=http#list-a-sites-drives){:target="_blank"} | SharePoint, OneDrive |
| Get driveItem<br>`https://graph.microsoft.com/v1.0/drives/<drive_id>/root/delta` | Files.Read.All | List all the items within a drive (change-based, as per Microsoft's scanning guidance) | [Get driveItem - Microsoft Graph API](https://learn.microsoft.com/en-us/graph/api/driveitem-delta?view=graph-rest-1.0&tabs=http){:target="_blank"} | SharePoint, OneDrive |
| Get driveItem resource<br>`https://graph.microsoft.com/v1.0/drives/<drive_id>/items/<item_id>` | Files.Read.All | Retrieve metadata for an item in a specified drive. | [Get driveItem resource - Microsoft Graph API](https://learn.microsoft.com/en-us/graph/api/driveitem-get?view=graph-rest-1.0&tabs=http){:target="_blank"} | SharePoint, OneDrive |
| Download file<br>`https://graph.microsoft.com/v1.0/drives/<drive_id>/items/<item_id>/content` | Files.Read.All | Fetch the contents of an item to index its body. | [Download file - Microsoft Graph API](https://learn.microsoft.com/en-us/graph/api/driveitem-get-content?view=graph-rest-1.0&tabs=http){:target="_blank"} | SharePoint, OneDrive |
| Get permissions<br>`https://graph.microsoft.com/v1.0/drives/<drive_id>/items/<item_id>/permissions` | Files.Read.All | Get the permissions of a given item within a drive. | [Get permissions - Microsoft Graph API](https://learn.microsoft.com/en-us/graph/api/driveitem-list-permissions?view=graph-rest-1.0&tabs=http){:target="_blank"} | SharePoint, OneDrive |


## Activity Endpoints

| Endpoint | Permissions | Use Case | Documentation | Product |
|---|---|---|---|---|
| Create subscription<br>`https://webhook.azurewebsites.net/api/send/<client>` | Files.ReadWrite.All | Create a change notification subscription to a given drive (driveItem). | [Create subscription - Microsoft Graph API](https://learn.microsoft.com/en-us/graph/api/subscription-post-subscriptions?view=graph-rest-1.0&tabs=http){:target="_blank"} | SharePoint, OneDrive |

!!! warning
    Without webhooks, new changes within user drives can take up to a day to be processed (via incremental crawling), compared to within ~1 hour with the webhook.

