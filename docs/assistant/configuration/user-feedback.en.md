---
icon: material/comment-alert-outline
title: "Receive User Feedback"
description: "Users can upvote or downvote Glean Assistant responses to provide feedback, and you can opt to have this feedback sent to a company email for review."
lang: en
tags:
    - "assistant"
    - "feedback"
authors:
    - "Nathan Catania"
---

Users can provide feedback to Glean Assistant responses as positive (👍) or negative (👎) with accompanying comments. You can opt to have this feedback sent to a company email for review.

## Configuration

!!! tip
    Glean recommends that you configure a separate alias for this to assist in routing and reviews. You may also wish to automatically ingest this feedback into a ticketing system like Jira, Zendesk, or ServiceNow.

To configure feedback emails:

1. Select the [Settings](https://app.glean.com/admin/setup/gleanassistant?tab=settings){:target="_blank"} tab under the settings for Glean Assistant.
2. Expand the **Feedback emails** dropdown, and populate the destination email address.

For security purposes, you are only able to enter an email address belonging to your company's domain. If you do not see the domain you wish to send the feedback to present, please contact Glean Support to have it added.