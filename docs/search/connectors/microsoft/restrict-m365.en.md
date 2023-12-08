---
icon: material/timer-stop
title: "Restricting Content"
description: "The Glean Atlassian connectors enable secure and efficient data fetching from Confluence and JIRA."
lang: en
tags:
    - "microsoft"
    - "sharepoint"
    - "onedrive"
    - "teams"
    - "outlook"
    - "content restrictions"
    - "connectors"
authors:
  - Nathan Catania
sources:
  - https://docs.google.com/document/d/1vCbHuZAZ-FK9iRudoGMTOScrshatwzKpPih7ZNmenw8/edit
---
# M365 Connector Support for Content Restrictions

## Overview
* **Green list** restrictions permit Glean to _only_ crawl and index specified content (specific include).
* **Red list** restrictions permit Glean to crawl and index everything _except_ the specified content (specific exclude).

| Restriction Type           | Green list | Red list | Details                                                                                                                           |
|----------------------------|-----------|-----------|-----------------------------------------------------------------------------------------------------------------------------------|
| Time-based Restrictions    | ✅        | ❌        | Restrict crawling to include/exclude content created/modified/viewed after a certain date.                                        |
| User-based Restrictions    | ✅        | ✅        | Restrict crawling to include/exclude content created/modified/viewed by specific users or a specific group (plus public content). |
| Content-based Restrictions | ✅        | ✅        | Restrict crawling to include/exclude specific content, documents, messages, or objects (see below).                               |

## Supported Restrictions

### SharePoint
| Restriction                | Green list | Red list | Details                                                                                                          |
|----------------------------|-----------|-----------|------------------------------------------------------------------------------------------------------------------|
| Date                       | ✅        | ❌        | Restrict crawling to only content created/modified/viewed after a specific date.                                 |
| Group                      | ✅        | ❌        | Restrict crawling to only content created/modified/viewed by users in a specific AD group (plus public content). |
| Site                       | ✅        | ✅        | Restrict crawling to include/exclude specific SharePoint sites.                                                  |

!!! info
    Sites should be provided in URL format without a trailing forward slash. Eg:
        ```
        https://<domain>.sharepoint.com/sites/<siteName>
        ```
    
    For Group restrictions when using Azure AD/Entra ID, the Object ID of the AD Group should be provided, NOT the Group name. Eg:
        ```
        7c77a355-c78c-6362-a195-d2428d285107
        ```

### OneDrive
| Restriction                | Green list | Red list | Details                                                                                                          |
|----------------------------|-----------|-----------|------------------------------------------------------------------------------------------------------------------|
| Date                       | ✅        | ❌        | Restrict crawling to only content created/modified/viewed after a specific date.                                 |
| Group                      | ✅        | ❌        | Restrict crawling to only content created/modified/viewed by users in a specific AD group (plus public content). |
| User                       | ✅        | ✅        | Restrict crawling to include/exclude specific user drives (by username)                                           |

!!! info
    For Group restrictions when using Azure AD/Entra ID, the Object ID of the AD Group should be provided, NOT the Group name. Eg:
        ```
        7c77a355-c78c-6362-a195-d2428d285107
        ```

### Teams
| Restriction                | Green list | Red list | Details                                                                                                          |
|----------------------------|-----------|-----------|------------------------------------------------------------------------------------------------------------------|
| Group                      | ✅        | ❌        | Restrict crawling to only content created/modified/viewed by users in a specific AD group (plus public content). |
| Channel                    | ✅        | ❌        | Restrict crawling to only the specified channel IDs                                                              |

!!! info
    For Group restrictions when using Azure AD/Entra ID, the Object ID of the AD Group should be provided, NOT the Group name. Eg:
        ```
        7c77a355-c78c-6362-a195-d2428d285107
        ```
    
    For Channel restrictions, you must specify the Channel ID, not the Channel Name.


### Outlook
Glean uses Outlook's federated search API to support searching over emails/calendars, so it does not index any of the Outlook emails or calendar events. Hence, there is no data stored to apply indexing restrictions to.


## Applying Restrictions
| Method                     | Supported | Details                                                                        |
|----------------------------|-----------|--------------------------------------------------------------------------------|
| Admin UI                   | ✅        | Restrictions can be applied in the Admin UI under the connector configuration. |
| Glean Support              | ✅        | Restrictions can be applied by Glean support on request.                       |

!!! warning
    Not all restrictions can be applied in the Admin UI. Please contact Glean support to apply the restriction if it is missing from the UI.