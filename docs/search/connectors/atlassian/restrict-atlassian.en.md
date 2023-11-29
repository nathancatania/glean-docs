---
icon: material/timer-stop
title: "Restricting Content"
description: "The Glean Atlassian connectors enable secure and efficient data fetching from Confluence and JIRA."
lang: en
authors:
  - Greg Bakken
  - Nathan Catania
sources:
  - https://docs.google.com/document/d/1vCbHuZAZ-FK9iRudoGMTOScrshatwzKpPih7ZNmenw8/edit
---
# Atlassian Connector Support for Content Restrictions

## Overview
* **Inclusion** restrictions permit Glean to only crawl and index specified content (specific include).
* **Exclusion** restrictions permit Glean to crawl and index everything except the specified content (specific exclude).

| Restriction Type           | Inclusion | Exclusion | Details                                                                                                                           |
|----------------------------|-----------|-----------|-----------------------------------------------------------------------------------------------------------------------------------|
| Time-based Restrictions    | ❌        | ❌        | Restrict crawling to include/exclude content created/modified/viewed after a certain date.                                        |
| User-based Restrictions    | ❌        | ✅        | Restrict crawling to include/exclude content created/modified/viewed by specific users or a specific group (plus public content). |
| Content-based Restrictions | ✅        | ✅        | Restrict crawling to include/exclude specific content, documents, messages, or objects (see below).                               |

## Supported Restrictions

### JIRA
| Content                    | Inclusion | Exclusion | Details                                                    |
|----------------------------|-----------|-----------|------------------------------------------------------------|
| Project                    | ✅        | ✅        | Restrict crawling to include/exclude specific Project IDs. |

### Confluence
| Content                    | Inclusion | Exclusion | Details                                                                                            |
|----------------------------|-----------|-----------|----------------------------------------------------------------------------------------------------|
| Spaces                     | ✅        | ✅        | Restrict crawling to include/exclude specific Confluence Spaces.                                   |
| Pages                      | ❌        | ✅        | Restrict crawling to exclude pages and blogposts with certain labels, or content matching a regex. |
| Creators                   | ❌        | ✅        | Restrict crawling to exclude content created by specific users.                                    |

## Applying Restrictions
| Method                     | Supported | Details                                                                        |
|----------------------------|-----------|--------------------------------------------------------------------------------|
| Admin UI                   | ✅        | Restrictions can be applied in the Admin UI under the connector configuration. |
| Glean Support              | ✅        | Restrictions can be applied by Glean support on request.                       |