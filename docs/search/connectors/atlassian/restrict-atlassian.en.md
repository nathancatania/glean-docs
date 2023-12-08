---
icon: material/timer-stop
title: "Restricting Content"
description: "You can apply restrictions to the content that Glean crawls (or does not crawl)."
lang: en
tags:
    - "atlassian"
    - "jira"
    - "confluence"
    - "content restrictions"
    - "connectors"
authors:
  - Nathan Catania
sources:
  - https://docs.google.com/document/d/1vCbHuZAZ-FK9iRudoGMTOScrshatwzKpPih7ZNmenw8/edit
---

# Atlassian Connector Support for Content Restrictions

## Overview
* **Green list** restrictions permit Glean to _only_ crawl and index specified content (specific include).
* **Red list** restrictions permit Glean to crawl and index everything _except_ the specified content (specific exclude).

| Restriction Type           | Green list | Red list | Details                                                                                                                            |
|----------------------------|-----------|-----------|------------------------------------------------------------------------------------------------------------------------------------|
| Time-based Restrictions    | ❌        | ❌        | Restrict crawling to include/exclude content created/modified/viewed after a certain date.                                         |
| User-based Restrictions    | ❌        | ✅        | Restrict crawling to include/exclude content created/modified/viewed by specific users or a specific group (plus public content).  |
| Content-based Restrictions | ✅        | ✅        | Restrict crawling to include/exclude specific content, documents, messages, or objects (see below).                                |

## Supported Restrictions

### JIRA
| Restriction                | Green list | Red lis  | Details                                                      |
|----------------------------|-----------|-----------|--------------------------------------------------------------|
| Project                    | ✅        | ✅        | Restrict crawling to include/exclude specific Project IDs. |

### Confluence
| Restriction                | Green list | Red list | Details                                                                                             |
|----------------------------|-----------|-----------|-----------------------------------------------------------------------------------------------------|
| Spaces                     | ✅        | ✅        | Restrict crawling to include/exclude specific Confluence Spaces.                                    |
| Pages                      | ❌        | ✅        | Restrict crawling to exclude pages and blog posts with certain labels, or content matching a regex. |
| Creators                   | ❌        | ✅        | Restrict crawling to exclude content created by specific users.                                     |

## Applying Restrictions
| Method                     | Supported | Details                                                                        |
|----------------------------|-----------|--------------------------------------------------------------------------------|
| Admin UI                   | ✅        | Restrictions can be applied in the Admin UI under the connector configuration. |
| Glean Support              | ✅        | Restrictions can be applied by Glean support on request.                       |

!!! warning
    Not all restrictions can be applied in the Admin UI. Please contact Glean support to apply the restriction if it is missing from the UI.