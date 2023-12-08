---
title: Crawling Strategy
description: "The Glean crawling system optimizes for minimizing the latency in incorporating updates in the source application while keeping the API call volume within rate limits and not overloading the source application."
lang: en
authors:
    - Raymond Carino
    - Nathan Catania
sources:
    - https://docs.google.com/document/d/1bHgu6ObRKcPH8KRvo7Rt0vTd4vs9PrJOEwhlQQaRKWg/edit
---

The Glean crawling system optimizes for minimizing the latency in incorporating updates in the source application while keeping the API call volume within rate limits and not overloading the source application.

## Per-app Frequencies
All the frequencies here are configurable and the values mentioned are the default frequencies based on feedback from customers. In addition, the customer can fully configure the API call rate (i.e. API calls/sec) as well as the number of concurrent API calls that are being made. In case the application responds with an error indicating it is overloaded then Glean does an exponential backoff dynamically.

In addition, Glean supports configuring different rates for different days/times of the day to enable customers to control the API load on their application for peak hours vs off-peak hours.

### Asana
* Incremental content crawl every 10 minutes
* Full content crawl every 28 days
* Identity crawl runs hourly
* Activity crawl every 10 minutes

### Azure
* People data crawled every hour
* People data indexed after an additional hour

### BambooHR
* People data crawled every hour
* People data indexed after an additional hour

### Confluence 
* Webhooks from Atlassian when a page is modified/added etc and trigger a crawl for the page accordingly typically within 5 minutes. 
* Incremental crawl every 1 hour for public pages (added reliability from the Webhooks).
* Full crawl of the corpus every 2 days.

### Figma
* Full crawls only ingest and show results to users who have explicitly authorized their Figma accounts with Glean.
* Default full crawl is every half hour.
* Identity crawl runs every half hour.

### GitHub
* Webhooks when a PR, issue, or comment is modified/added trigger a crawl for that content typically within 5 minutes. 
* Incremental crawl (PRs, issues, comments as well as git pull) every 10 minutes.
* Full crawl of all repositories every 28 days.

### Gmail
* We do not crawl any data but hit the federated API directly.

### Google Drive (GDrive)
* Activity reports (adds/updates/permissions changes etc) every 10 minutes and crawl the modified content based on that.
* Incremental crawl every 3 hours (added reliability from the 10-minute activity reports).
* Full crawl of the corpus every 28 days.
* People data crawled every hour.
* People data indexed after an additional hour.

### Google Sites
* Default full crawl is every 28 days.
* Incremental crawl runs every 4 hours.

### Jira
* Webhooks from Atlassian when an issue/comment is modified/added/deleted and trigger a crawl for the page accordingly typically within 5 minutes.
* Incremental crawl every 3 hours.
* Full crawl of the corpus every 7 days.

### Lattice
* People data crawled every hour
* People data indexed after an additional hour

### Monday.com
* Default full crawl is every hour.

### Notion
* Default full crawl is every 6 hours.
* Does not have incremental crawl
* Identity crawl every hour.

### Okta
* Full crawl every 3 hours
* People data indexed after an additional hour
* Activity crawl every hour (if enabled)

### OneDrive
* See SharePoint.

### Salesforce
* Default full crawl is every 28 days.
* Incremental crawl runs every 10 minutes.
* Identity crawl runs hourly.
* Entity crawl runs daily.

### ServiceNow
* Incremental content crawl (Knowledge Articles) every hour.
* Full content crawl (Knowledge Articles) every 3 days.
* Full content crawl (Catalog Items) every 30 mins with identity.
* Identity crawl every 30 mins.
* Activity crawl every 30 mins.

### Sharepoint
* Activity reports (adds/updates/permissions changes etc) every 10 minutes.
* Incremental crawl every hour (added reliability from the 10-minute activity reports).
* Full crawl of the corpus every 28 days.

### Slack
* Webhooks from Slack for new messages/deletes/edits etc and we crawl the particular message accordingly typically within 5 minutes.  
* Incremental crawl every 3 hours (added reliability from the Webhooks).
* Full crawl of the corpus every 28 days.

### Slack Enterprise Grid
* Activity crawl every minute for new messages/deletes/edits etc and we crawl the particular message accordingly typically within 5 minutes.  
* Full crawl of the corpus every 28 days.

### Stackoverflow
* Default full crawl is every 28 days.
* Incremental crawl is every 3 hours.
* Identity crawl every hour.

### Websites (Web Crawler)
* Full crawl daily

### Zendesk
* Default full crawl is every 28 days.
* Incremental crawl is hourly.
* Identity crawl every hour.


## Data Refresh Rates
| Datasource                  | Average SLA            | P90 SLA                | Notes                                                                                                                                                                                                                                                                                                |
| --------------------------- | ---------------------- | ---------------------- | ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| Box                         | 15 mins                | 1 hour (configurable)  | The system uses Events API to identify new/modified/deleted docs every 10 minutes and reprocesses them. In case the API has a delay in returning modified items, the system does an incremental fetch every hour to catch up on the changes                                                          |
| Confluence Datacenter       | 5 minutes (\*)         | 1 hour                 | For newer versions of Confluence Datacenter that offer webhooks, the system can incorporate changes in the content in 5 minutes. It also does an incremental fetch every 1 hour, that addresses older versions of Confluence.<br>New permissions to the service account are reflected within 2 days. |
| GDrive                      | 15 minutes             | 3 hours (configurable) | The system uses Reports API to identify new/modified/deleted docs every 10 minutes and reprocesses them. In case the API has a delay in returning modified items, the system does an incremental fetch every 3 hours to catch up on the changes                                                      |
| Internet/Intranet web pages | 1 day (configurable)   |                        | By default the system crawls configured web pages once daily but this is completely configurable                                                                                                                                                                                                     |
| Jira Datacenter             | 5 minutes              | 3 hours (configurable) | The system uses webhook events to react to ticket changes in 5 minutes. For edge cases where the webhook is not delivered on time, the system does an incremental fetch every 3 hours (configurable) to incorporate changes.                                                                          |
| Onedrive / Sharepoint       | 1 hour                 |                        | The system uses User Insights API to identify new/modified/deleted docs every 10 minutes. The system does an incremental fetch every hour to catch up on the changes                                                                                                                                 |
| People Data API             | 1 hour                 |                        | Data can be uploaded or modified at any time using the push API. Changes will be reflected in the product at a 1-hour cadence.                                                                                                                                                                          |
| Push API for Content        | Fully configurable     |                        | For custom datasources pushed using the Push API, the customer controls the frequency of updates. The system offers both bulk upload APIs (for periodic full synchronization of the data) as well as Create/Update/Delete of individual items for real-time updates.                                 |
| Salesforce                  | 15 mins                |                        | The system does an incremental fetch every 10 mins to fetch created/updated/deleted objects from Salesforce.                                                                                                                                                                                         |
| ServiceNow                  | 3 days (configurable)  |                        | The system does a full refresh of Knowledge Articles every day for ServiceNow. The refresh can be configured more frequently if needed.                                                                                                                                                              |
| Slack                       | 5 minutes              | 3 hours (configurable) | The system uses webhook events to react to new/edited/deleted messages and files. It also does an incremental fetch every 3 hours (configurable) to address cases where the webhook was not delivered on time.                                                                                       |
| Stack Overflow              | 3 hours (configurable) |                        | By default the system fetches incremental changes every 3 hours but this is configurable                                                                                                                                                                                                             |
| Zendesk                     | 1 hour (configurable)  |                        | The system does an incremental fetch every 1 hour to fetch created/updated/deleted objects from Zendesk.                                                                                                                                                                                             |

## Deletion of Content
The above content also applies to the deletion of content in the source applications, since the datasource APIs and webhooks convey deleted content in most major applications. Some applications don't have this information, and in these cases, the stale content is deleted every time a full crawl is performed.

Deletion of other derived information (used in models etc) is governed by Glean’s [privacy policy](https://www.glean.com/privacy-policy).