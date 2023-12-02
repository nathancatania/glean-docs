---
icon: material/hammer-wrench
title: JIRA Configuration
description: Step-by-step instructions on how to connect Glean to your JIRA instance.
lang: en
authors:
  - Nathan Catania
sources:
  - https://docs.google.com/document/d/1vCbHuZAZ-FK9iRudoGMTOScrshatwzKpPih7ZNmenw8/edit
---
# JIRA Connector Configuration

## 1. Install the Glean app
1. Go to [https://marketplace.atlassian.com/apps/1222715/glean-crawler-for-jira](https://marketplace.atlassian.com/apps/1222715/glean-crawler-for-jira)
2. Click **Get it now**.
3. Select the Jira site you're connecting, click **Install App** and complete the installation process.
	
	![https://app.glean.com/images/admin/jira-cloud/install-app.png](https://app.glean.com/images/admin/jira-cloud/install-app.png)

## 2. Set up the basics
1. Sign into Jira as an admin. Copy your Atlassian domain from the URL bar and paste into Glean:
	```
	https://<your_atlassian_domain>.atlassian.net
	```

2. Go to [https://admin.atlassian.com](https://admin.atlassian.com)

3. Click the 3 dots belonging to the organization matching your Atlassian domain from step 1, then click on **Manage product access**.
4. Click on **Manage access for the Jira Software Product**.
5. Enter the default groups (there might be only one) as a comma-separated list in Glean.
	
	!!! warning
		Only users in the provided product access groups will be able to see results in Glean.

6. 6. Click **Save** in Glean.

![https://app.glean.com/images/admin/jira-cloud/default-group.png](https://app.glean.com/images/admin/jira-cloud/default-group.png)

## 3. Configure Webhook and Activity Plugin
### 3a. Connect the Webhook
1. After clicking **Save** in Glean in the previous section, refresh the page in your browser. This will allow the newly generated webhook link to be fetched and populated (in Step 5 below).
2. Go back to Jira, i.e. `https://<your_atlassian_domain>.atlassian.net/jira`, click on the Settings gear in the top right corner, then click **Apps > Manage apps**.
3. Click on Settings near the bottom of the page and ensure **Enable development mode**  and **Enable private listings** are selected. Click **Apply** and refresh the page.
4. Click on **Upload app** near the top right of the page.
5. When viewing these instructions in the Glean Admin UI, a unique Webhook URL will be displayed. Copy and paste it into the box that appears in the JIRA interface. The URL will be of the form:
	```
	https://marketplace.atlassian.com/files/1.0.0-AC/XXXXXXXX-XXXX-XXXX-XXXX-XXXXXXXXXXXX
	```
6. Click **Upload**.

## 3b. Install the Activity Plugin
1. Go to [https://marketplace.atlassian.com/apps/1229003/glean-activity-plugin-for-jira-cloud](https://marketplace.atlassian.com/apps/1229003/glean-activity-plugin-for-jira-cloud){:target="_blank"}.
2. Click **Get it now**.
3. Select the Jira site you're connecting, and click **Install App** to complete the installation process.

!!! success
	The JIRA connector is now configured. You can either start a crawl, or configure what content should be included/excluded from the crawl.
