---
icon: material/information
title: "Overview"
description: "The Glean Microsoft 365 connectors enable secure and efficient data fetching from OneDrive, SharePoint, Teams, and Outlook"
lang: en
authors:
  - Rick Huang
  - Nathan Catania
sources:
  - https://docs.google.com/document/d/1togE17FHUhqVKInvUozCFWob4ehRiRza0L3XSp93_9g/edit
  - https://docs.google.com/document/d/1fIWENEwwubo6dh-NO06iZ2MY6U970vUlMZSD-xehusE/edit
---
# Microsoft 365 Connector Overview

## About the M365 Connector
The Glean M365 connectors enable secure and efficient data fetching from OneDrive, SharePoint, Teams, and Outlook. User permissions are strictly enforced and all data remains securely within your environment.

* Glean requires authentication to the O365 instance in order to fetch relevant information.
* Authentication is done by creating and registering an App Registration for each deployment.
    * More information: [Auth V2 Service (docs.microsoft.com)](https://docs.microsoft.com/en-us/graph/auth-v2-service){:target="_blank}
* Glean understands all user access permissions and strictly enforces permissions for users at the time of the query. This ensures that users are not able to see results which they do not have access to.
* Quicklinks are provided to quickly create Word, Excel, and PowerPoint documents in OneDrive.


## Integration Features
Glean currently uses the Graph API v1.0 to ingest all data and permissions, using the current Microsoft Graph API SDK v5.30.0.

### OneDrive
For OneDrive, Glean indexes the following content:

* Folders
* Documents (All document types, e.g. Word, Excel, PowerPoint)
* OneNote (limited support, indexing Notebooks + Sections)

### SharePoint
For SharePoint, Glean indexes the following content:

* Site Pages
* Site Drives

### Teams
For Teams, Glean indexes the following content:

* Conversations in channels (public and private)
* Files shared in channels (public and private)
* Chat messages
* Private conversations (DMs) (optional opt-in)

### Outlook
Glean uses Outlook's federated search API to support searching over emails/calendar, so it does not index any of the Outlook emails or calendar events.




## API Usage & Permissions
Glean will use the standard Graph API v1.0 and [Sharepoint REST API](https://docs.microsoft.com/en-us/sharepoint/dev/sp-add-ins/get-to-know-the-sharepoint-rest-service?tabs=csom){:target="_blank} to ingest data. We use application permissions with admin granted access.

Glean uses the recommended [best practices](https://docs.microsoft.com/en-us/onedrive/developer/rest-api/concepts/scan-guidance?view=odsp-graph-online){:target="_blank} strategy provided by Microsoft to both crawl and record incremental changes for all documents.

### OneDrive & SharePoint
The Glean app, set up by the tenant administrator for Onedrive/Sharepoint, will require the following permissions:

For identities (application permissions):

* User.Read.All
* Group.Read.All
* GroupMember.Read.All

For content and activity (application permissions):

* Directory.Read.All
* Files.Read.All
* Files.ReadWrite.All (for webhooks)
* Reports.Read.All (for ranking signals)
* Sites.Read.All
* Sharepoint permissions as listed in the configuration steps, require full control over Site Collections to properly crawl all Sharepoint site content and permissions via REST.

### Teams
For identities (application permissions):

* User.Read.All
* Group.Read.All
* GroupMember.Read.All

For content and activity (application permissions):

* Channel.ReadBasic.All
* ChannelMember.Read.All
* ChannelMessage.Read.All
* ChannelSettings.Read.All
* Chat.Read.All
* Chat.ReadBasic.All
* Team.ReadBasic.All
* TeamMember.Read.All
* TeamSettings.Read.All
* Files.Read.All
* TeamsTab.Read.All
* Directory.Read.All

Glean subscribes to webhooks on channel messages to refresh the index with the latest messages.
Glean also augments webhook events with incremental updates to all channels.

!!! tip
    Glean does not expect to use any paid APIs for the Microsoft Teams integration.
  
    The paid APIs often represent endpoints that bulk export all messages from channels and chats from the given instance, whereas Glean indexes based on a per-channel, per-chat method.

### Outlook
For content (application permissions):

* Mail.Read
* Calendars.Read





## Setup Prerequisites
A tenant administrator (global admin privileges for both Azure portal and Sharepoint admin) is required to set up several dedicated service applications granted with the required privileges above.
