---
icon: material/information
title: "Overview"
description: "The Glean Atlassian connectors enable secure and efficient data fetching from Confluence and JIRA."
lang: en
authors:
  - Greg Bakken
  - Nathan Catania
sources:
  - https://docs.google.com/document/d/1vCbHuZAZ-FK9iRudoGMTOScrshatwzKpPih7ZNmenw8/edit
---
# Atlassian Connector Overview

## About the Atlassian Connector
The Glean Atlassian connectors enable secure and efficient data fetching from Confluence and JIRA, indexing various content types, and strictly enforcing user access permissions, all while ensuring data remains within the customer's environment.

* Glean requires authentication to the Atlassian instance in order to fetch relevant information from Confluence and JIRA.
* For Confluence/Jira Cloud, the Atlassian admin needs to install Glean’s Atlassian Connect apps to the instance. For Confluence/Jira Data Center authentication is done by creating a dedicated user account in Atlassian and authenticating with the username/password.
* Glean understands all user access permissions and strictly enforces permissions for users at the time of the query which ensures that users are not able to see results which they do not have access to.
* It’s important to note that all data is stored in a GCP project inside the customer’s cloud account and no data leaves the customer's environment.

## Integration Features
For JIRA, Glean indexes the following content:

* Projects 
* Issues 
* Comments
* Dashboards
* Filters

For Confluence, Glean indexes the following content:

* Spaces
* Pages
* Blogs
* Comments - from both Pages and Blogs

For Service Management, Glean indexes the following content:

* Requests / Tasks
* Request Types

## API Usage
Glean will use the standard API to ingest all data. For Service Management, Glean uses the Service Desk API to ingest request types.

In order to capture changes as quickly as possible, Glean will deploy a webhook that will send push notifications to an endpoint deployed within your Glean tenant.

## Setup Prerequisites
In order to set up Atlassian connectors, administrator permissions are required in order to get user emails for identity and permissions enforcement within Glean.

When Atlassian admins grant administrator permissions for Glean, Atlassian adds write & delete permissions to the scope, which is noted in our Atlassian Marketplace app page. **Glean does not use the write or delete permissions in the scope since our operations are read-only.**

=== "Cloud version"
    The Jira/Confluence admin will install an Atlassian Marketplace app with Admin scope.
    
    !!! info
        Glean requires Admin scope in order to fetch permissions associated with Jira objects. This is required for the enforcement of permissions within search.
        
        The Admin scope is also used to create another connect app that delivers webhooks to your Glean instance. Webhooks allow your Jira instance to notify Glean when an object changes; reducing the time for changes to reflect in Glean search results.

    Installing the Glean connect app for Confluence will allow the app to read all unrestricted pages in these spaces. It will not be able to read restricted pages unless the admin grants access to the Glean app for those pages.

=== "Data Center version"
    Create a new user account that has access to all content in both JIRA and Confluence. Use this account to create an API token as listed below.

    * The user account needs “Administer Project” permissions for all Jira projects that need to be indexed.
    * The user accounts need to be added to all Confluence spaces that need to be indexed, and there needs to be an admin in all those spaces (in order to be able to fetch the space permissions used to enforce permissions-aware search over Confluence)

    !!! warning
        Atlassian does not have the ability to create a service account, so you will need to create a new user account which will most likely require that your GSuite or SSO admin is also present so that they can create a new user in that system.
        
        The user account needs to be an Administrator in Jira. This is needed to be able to enumerate all users who have Jira product access.

    In addition, you must provide Glean with the IP address of the server or load balancer.

    **Minimum Version Requirements for DC version**
    
    | Confluence                |                |
    |---------------------------|----------------|
    | Crawls (identity/content) | v7.4 and later |
    | Webhooks                  | v7.7 and later |
    | Activity plugin           | v7.4 and later |

    | Jira                      |                |
    |---------------------------|----------------|
    | Crawls (identity/content) | v7.4 and later |
    | Webhooks                  | v7.5 and later |
    | Activity plugin           | v7.4 and later |

