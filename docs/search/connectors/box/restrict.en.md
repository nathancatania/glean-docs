---
icon: material/timer-stop
title: "Restricting Content"
description: "Mechanisms available to limit the content that Glean indexes for Box."
---
# Box Connector Support for Content Restrictions

## Overview
* **Green list** restrictions permit Glean to _only_ crawl and index specified content (specific include).
* **Red list** restrictions permit Glean to crawl and index everything _except_ the specified content (specific exclude).

| Restriction Type           | Green list | Red list | Details                                                                                                                           |
|----------------------------|-----------|-----------|-----------------------------------------------------------------------------------------------------------------------------------|
| Time-based Restrictions    | ✅        | ❌        | Restrict crawling to include/exclude content created/modified/viewed after a certain date.                                        |
| User-based Restrictions    | ❌        | ✅        | Restrict crawling to include/exclude content created/modified/viewed by specific users or a specific group (plus public content). |
| Content-based Restrictions | ❌        | ✅        | Restrict crawling to include/exclude specific content, documents, messages, or objects (see below).                               |

## Supported Restrictions

| Restriction                | Green list | Red list | Details                                                                                                          |
|----------------------------|-----------|-----------|------------------------------------------------------------------------------------------------------------------|
| Date                       | ✅        | ❌        | Restrict crawling to only content created/modified/viewed after a specific date, e.g. `YYYY-MM-DD`               |
| User (Owner)               | ❌        | ✅        | Restrict crawling to exclude content owned by specific users.                                                    |
| Content (Folder)           | ❌        | ✅        | Restrict crawling to exclude content within specific folders.                                                    |
| Content (File)             | ❌        | ✅        | Restrict crawling to exclude specific files.                                                                     |

!!! info
    When specifying restrictions for Owners, Folders, or Files, the ID of the owner, folder, or file within Box must be specified. For example:

    Owner IDs:
        ```
        23400261190,23401260091 
        ```

    Folder IDs:
        ```
        119142000606,518142000607
        ```

    File IDs:
        ```
        31600504200,31600504201
        ```


## Applying Restrictions
| Method                     | Supported | Details                                                                        |
|----------------------------|-----------|--------------------------------------------------------------------------------|
| Admin UI                   | ❌        | Restrictions cannot currently be applied in the Admin UI.                      |
| Glean Support              | ✅        | Restrictions can be applied by Glean Support on request.                       |


## Limitations
### Folder & File Red Listing
Glean monitors the event feed for your Box environment to pick up new content and changes to existing content.

When a crawl of new content is triggered, there is currently no way for Glean to determine whether the new content is within a red listed folder or not. In this scenario, the new content will be crawled, even if the parent folder is red listed. This is corrected on the next full crawl.

Red listing via the Owner ID does not have this limitation.