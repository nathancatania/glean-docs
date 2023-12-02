---
title: About Connectors
description: "Glean connectors are integral components of the Glean platform, designed to fetch data and permissions from various enterprise data sources."
lang: en
authors:
  - Nathan Catania
sources:
  - https://docs.google.com/document/d/1fNxclCU23i8d8SqSAHbVs6ytPdwBMYK8um6aeMIJgwE/edit
  - 'Glean Chat (Write me a help article about Glean connectors. What are they, what do they do, why are they important, etc. Do not target any one specific connector. This is to be used as an "about" or "overview" page for all connectors.)'
---



Glean connectors are integral components of the Glean platform, designed to fetch data and permissions from various enterprise data sources. They serve as bridges between Glean and your organization's various data sources, enabling Glean to index and make searchable a wide range of content.

## What are Glean Connectors?
Glean connectors are tailor-made for each application's unique data model and API endpoints.

They are designed to fetch relevant information from various data sources, including but not limited to communication tools like Slack, Teams, Gmail, Outlook, and cloud storage platforms like OneDrive, Sharepoint, Box, Dropbox, and Drive.

Glean offers over 80 native connectors and supports the development of custom connectors through its developer platform.


## What Connectors does Glean support?
A list of all Glean connectors is [available here](https://www.glean.com/connectors){:target="_blank"}.


## What do Glean Connectors do?
Glean connectors perform two primary functions:

* **Content Parsing:** Connectors parse item content (e.g., title, body, comments, media) and permissions (i.e., who is allowed to view the item). This is done for native app content (e.g., Google Doc, Teams message) and all common file types (e.g., pdf, doc, ppt, xls, vsd).

* **Data Fetching:** Connectors fetch data from the source applications and store the fetched information into Glean’s system. They also fetch the permissions map from the source, ensuring that Glean search results strictly adhere to the access permissions set in the source application.


## Why are Glean Connectors important?
Glean connectors are crucial for several reasons:

1. **Comprehensive Connectivity:** With over 80 native connectors and the ability to develop custom ones, connectors allow Glean to connect to a wide range of applications in use throughout your organization, ensuring that all relevant enterprise data can be searched and accessed.

2. **Permission Enforcement:** By fetching the permissions map from each source, Glean connectors ensure that search results strictly adhere to the access permissions set in the source application. This ensures that users are not able to see results which they do not have access to.

3. **Data Security:** Connectors route all data fetched to your isolated Glean tenant. Data is end-to-end encrypted in transit, and only written to disk once it reaches your tenant. Once inside your tenant, data within your index is encrypted at rest and does not leave your tenant.

4. **Real-time Updates:** Connectors are designed to capture changes to your data as quickly as possible, either via a webhook or incremental crawling. The Glean team also continuously works with our technology partners to ensure that connectors are updated frequently to reflect any feature enhancements or API changes made in the source application.


## Types of Connectors
There are 3 types of Glean connectors:

### Native Connectors
Native connectors make up the vast majority of Glean connectors.  They are built specifically for a particular data source, like Google Drive, to directly interface with its API and index the data contained within it. Native connectors can crawl data extensively, support the crawling of attachments, can parse threaded results, support mentions for threads, and more!

Native connectors are only possible if the API of the data source fully supports reading all of the data that Glean needs to build our knowledge graph and provide quality search results. Specifically this includes:

1. **Content data**
    Eg: Documents, messages, tickets, images, entities, etc.
2. **People data**
    Eg: Identities, roles, permissions, groups, etc - Essentially, which users are able to access the data source itself and each piece of content within it.
3. **Activity data**
    Eg: When was each piece of content created, modified, edited, viewed, or shared and by whom?

### Web History Connectors
There are certain scenarios where a native connector might not exist for an app due to the following reasons:

- Glean has not yet built out a native connector.
- The data source does not support the functionality we need to build the knowledge graph (e.g., insufficient API).
- Crawling content would violate the Terms of Service (TOS) of the target service.

In these cases, and for specific apps, the Glean browser extension can be used to include browser history links as part of search results for these apps, thereby making search results more relevant for the user.

Glean will be able to search across the titles of the pages your employees have visited. However, because these are history-based results, users will only be able to view content that they have seen before in these workplace apps.

It's important to note that results from a user's browser history are completely secure and private to the individual user. The company will not be able to see results from a user's browser history.

### Push API Connectors
Glean offers multiple APIs for developers, one of which is an indexing API. This API allows our customers or partners to build their own connectors in situations where Glean does not have a native connector, or when there is a lack of an interface for Glean to pull data from normally. 

When you see a Push API connector referenced, it typically refers to one of the following scenarios:

- Code that has been developed to push data to Glean from within an app or environment due to a deficient interface, API or authentication process.
- Code that has been developed to push data to Glean from within an app or environment because it is self-hosted and not accessible inbound from the internet.
- Code that another customer or Glean partner has developed and shared with Glean under an MIT license (i.e., anyone can use the code without warranty).
