---
icon: material/api
title: "API Endpoints"
description: "The Glean Box connector enables secure and efficient data fetching from your enterprise Box tenant."
---

Glean leverages the following endpoints of the Box API to crawl and index content. All connectivity is made through the [Glean app available in the Box App Center](https://app.box.com/app-center/glean_search/app/gQSMcDoLbs){:target="_blank"}.

## Authentication Endpoints

| Endpoint | Use Case | Documentation Link |
|---|---|---|
| Refresh access token<br>`https://api.box.com/oauth2/token` | Refresh an Access Token using its client ID, secret, and refresh token. | [Refresh access token - Box API](https://developer.box.com/reference/post-oauth2-token--refresh/){:target="_blank"} |

## Identity Endpoints

| Endpoint | Use Case | Documentation Link |
|---|---|---|
| List enterprise users<br>`https://api.box.com/2.0/users` | Determine which users (and associated content) need to be indexed. | [List enterprise users - Box API](https://developer.box.com/reference/get-users/){:target="_blank"} |
| List groups for enterprise<br>`https://api.box.com/2.0/groups` | Fetch all groups within a tenant (for permissions). | [List groups for enterprise - Box API](https://developer.box.com/reference/get-groups/){:target="_blank"} |
| List Enterprise Users<br>`https://api.box.com/2.0//:group_id/memberships` | Determine which users are a member of which group (for permissions). | [List members of group - Box API](https://developer.box.com/reference/get-groups-id-memberships/){:target="_blank"} |

## Content Endpoints

| Endpoint | Use Case | Documentation Link |
|---|---|---|
| List items in folder<br>`https://api.box.com/2.0/folders/:folder_id/items` | List all items and content within a folder for indexing. | [List items in folder - Box API](https://developer.box.com/reference/get-folders-id-items/){:target="_blank"} |
| Get file information<br>`https://api.box.com/2.0/files/:file_id` | Retrieve metadata for each specific item for indexing. | [Get file information - Box API](https://developer.box.com/reference/get-files-id/){:target="_blank"} |
| List file collaborations<br>`https://api.box.com/2.0/files/:file_id/collaborations` | Retrieve a list of all users with access to an item (for permissions). | [List file collaborations - Box API](https://developer.box.com/reference/get-files-id-collaborations/){:target="_blank"} |
| Download file<br>`https://api.box.com/2.0/files/:file_id/content` | Fetch the contents of an item to index its body | [Download file - Box API](https://developer.box.com/reference/get-files-id-content/){:target="_blank"} |

## Activity Endpoints

| Endpoint | Use Case | Documentation Link |
|---|---|---|
| List user and enterprise events<br>`https://api.box.com/2.0/events` | Fetch activity data for each user for ranking signals (12 months limit). | [List user and enterprise events - Box API](https://developer.box.com/reference/get-events/){:target="_blank"} |