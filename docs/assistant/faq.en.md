---
title: "FAQ"
description: "A list of Frequently Asked Questions regarding Glean Assistant and Generative AI."
lang: en
tags:
    - "assistant"
    - "faq"
authors:
    - "Deedy Das"
    - "Vivek Choksi"
    - "Nathan Catania"
sources:
    - https://docs.google.com/document/d/1z5xEN6D92W2pLt0ezsmT68rZ9v9OsMGcUh0v9ple0Jw/edit
---

## Activation & Rollout
!!! quote "How do I get access to Glean Assistant?"

Glean Assistant can be enabled by navigating to [Workspace Settings > Setup > Assistant](https://app.glean.com/admin/setup/gleanassistant){:target="_blank"} and selecting **Activate**.

Note that if the option is greyed out, then either:

1. You need to finish setting up your Glean tenant first (including directory sync).
2. Glean Assistant is not available for activation at this time (try again later).

:octicons-arrow-right-24: More information: [Set Up Glean Assistant]().


!!! quote "Can it be enabled only for specific users?"

Yes, this is the preferred method of roll out.

:octicons-arrow-right-24: More information: [Set Up Glean Assistant]().


!!! quote "What usage statistics are available?"

We provide a whole host of metrics for Administrators under [Insights > Assistant](https://app.glean.com/insights/assistant) in the Admin UI.

Please reach out to Glean Support if there are any specific metrics that you would like to see. 


!!! quote "Is Glean Assistant Opt-In or Opt-Out?"

Glean Assistant is **Opt-In**. It is disabled by default.


!!! quote "We are not licensed for Glean Assistant. How much does it cost?"

This varies depending on whether or not you will use Glean's LLM API key or your own. Please contact Glean Support or reach out to your Glean Sales Team directly.


!!! quote "I want to use my own API key. How can I estimate usage and cost?"

For OpenAI GPT or Azure OpenAI GPT, the per-query cost is approximately USD $0.15-0.16.

:octicons-arrow-right-24: More information: [Estimating API Usage Costs]()

---

## Infrastructure

!!! quote "What LLMs does Glean use?"

GPT (GPT3.5+GPT4) and Google PaLM 2 (unicorn) are supported.

:octicons-arrow-right-24: More information: [Supported LLMs]().


!!! quote "Can I use my own LLM?"

No. You must use an LLM that Glean supports.

:octicons-arrow-right-24: More information: [Supported LLMs]().


!!! quote "Do you support using a custom LLM or a self-hosted on-prem model?"

No. You must use an LLM that Glean supports.

:octicons-arrow-right-24: More information: [Supported LLMs]().


!!! quote "Do you support custom tuning of your models?"

Not at this time.


!!! quote "Do you build vector stores of the data you index?"

Glean is powered by a hybrid vector and traditional IR index, which ranks documents personalized to your role, the people you work with, accounting for doc’s inherent popularity and accuracy. Glean is also fully permissions-sensitive on a document level. In our evaluation, this is far beyond the search quality a vector DB can provide.

We also offer a rich suite of operators (e.g. updated in the last week, authored by, edited by, etc) which make our search even more powerful than a vector DB.

---

## Privacy & Security

!!! quote "When using OpenAI/GPT as the LLM, is it possible to specify the region for OpenAI's servers?"

When using your own key, we can support any geography. When using Glean's own Azure OpenAI key, we leverage the East-US API endpoint region.


!!! quote "What is the architecture of your Generative AI products? Do you send data to LLMs?"

Glean Assistant interacts with the Glean Knowledge Graph on your behalf; only accessing data that the querying user would see. The user's natual language prompt is broken down into keywords that are used to fetch relevant data from the Knowledge Graph; just as we would when surfacing a traditional search result.

The user's query and text snippets from the relevant data fetches (documents, messages, etc) are then sent, completely encrypted, to the LLM for a response.

When using Glean's API key, 0-day data retention is guaranteed. Your data is never stored or written to disk when it reaches the LLM API endpoint, nor is your data ever used to train the LLM.


!!! quote "Do you use data to fine-tune LLMs?"

No, we do not use any of your corpus' data to fine-tune third-party LLMs. Furthermore, we have contractual guarantees from our LLM vendors that your data is not retained or used to train the respective LLM either.


!!! quote "What specific data is sent to the LLM API?"

We send the user's query, and the metadata and snippets from document results (as you would see them see them in Glean Search Results page) to the LLM API.

Metadata includes the author name, document title, date, document type and other details in the byline of the search results. Below is an example where the document is a meeting transcript stored in the datasource, Gong:

```json
{
    "owner": "Scott Kaufman",
    "snippets": [
        "I really need to start like putting a timer on my phone to move around because I feel like I haven't gotten up since like out of my seat since seven am that's not healthy. No, I just actually got, I just slipped my dog out back in and got some quick lunch. So, but yeah, I need to do the same. Yeah, this is my last call until lunch break and walk the dogs and all that stuff. So, I spoke to John on Tuesday. Have you had any contact with Ish, or Andrew? I have not… no, I haven't… Okay. So as far as I know the goal links fix went out this week? It did. They're still pointed to their old system right now"
    ],
    "title": "Grammarly—Glean sync",
    "updateTime": "2023-01-26",
    "url": "https://us-123.app.gong.io/call?id=123"
}

```

The specific snippets we attach are based on lexical and semantic matches of the question to your document to find the relevant section.


!!! quote "Does our data leak to other Glean customers? Is there the potential for other Glean customers to see our data?"

Absolutely not. Queries and snippets of your data can leave your deployment to go to our LLM provider with our privacy guarantees (0-day retention, no training).

There is no co-mingling of your data with other customers and we do not fine-tune models.

Glean operates a single tenant architecture where each Glean customer has their own infrastructure that is spun-up on tenant creation. All tenants are completely isolated from each other.


!!! quote "How can I ensure users only see information they have access to?"

Glean enforces permissions that you set on underlying documents. All answers are only generated with search results visible to the user. If permissions on any underlying document changes, Glean's system recognizes that within minutes and updates.


!!! quote "Generative AIs commonly hallucinate. How can I guarantee that the answer is accurate?"

While it is known that generative AI technologies like large language models are prone to hallucination, our Generative AI features minimize the extent of this hallucination by grounding the generation on the content of your documents. Glean employs various techniques to make your generative output more deterministic (consistent from run to run) as well as specifically to ground its output in documents.

For AI Answers and Glean Chat, we ensure that all responses include citations that link to the relevant snippets in the source document so you can verify the authority of the response you get.

There are several key types of hallucinations we monitor for:

* **Hallucinating information not present in docs** — We measure this and rarely see this type of information.
* **Omitting key information present in docs** — This happens infrequently, but is more common for answers where a complete answer would take 500+ words to accurately describe. Please report this to us if you see such cases.
* **Hallucinating because one of the underlying docs is stale or incorrect** — This can happen, and citations are meant to ensure that the user knows which doc was used. Users have control over the datasources that are used for answer generation (default: all available datasources), and you can use [exclusions](){:target="_blank"} and [custom instructions](){:target="_blank"} to help fine-tune responses for your employees.


!!! quote "Does Glean plan to have an LLM completely hosted within the customer tenant?"

Glean hosts customer tenants on Google Cloud Platform (GCP) and is able to facilitate this if Google PaLM 2 is selected as the LLM to be used for Glean Assistant. This ensures that no data leaves your tenant.

As for hosting alternative models within the tenant, today this is not feasible due to the quality of responses self-hosted models tend to provide, however we do periodically re-assess this.


!!! quote "What is the granularity at which I can control the data being sent to the LLM APIs? Can I control and mandate that all PII be obfuscated?"

The answers above describe the data that we send in the request to the LLM. At this time, we do not offer levers to control this granularity. Removing PII from the request would render the result useless to the user.

As a reminder, all data sent to the LLM for a given query is only that which the querying user has permission to access. We have contractual guarantees that no content sent to the LLM is ever logged or used for training purposes.

While Azure Open AI has support for [content filtering](https://learn.microsoft.com/en-us/azure/cognitive-services/openai/concepts/content-filter){:target="_blank"}, we have observed a drastic reduction in response quality when it is enabled. We recommend using a combination of [exclusions](){:target="_blank"} and [custom instructions](){:target="_blank"} on the Glean side to control output and what is sent to the LLM.


!!! quote "What data do you log and how long is it retained?"

All logs are stored within your isolated tenant, with the exception of some strictly anonymous data that is used for metrics and product enhancements (e.g. What % of users access Glean Assistant via the search box vs the dedicated Chat menu?)

**Within your deployment**

Retention: 270 days

Sink: Google Cloud Storage (GCS)

Access to the deployment and logs therein is only granted in response to an explicit customer request to debug issues. These logs capture:

* Timestamp
* Tracking tokens
* User ID
* Author type ("glean" OR "user")
* Platform
* Initiator (Surface)
* Latency time
* Error and type
* Message contents
* Upvote or Downvote
* Manual feedback message


**Scrubbed logs exported to Glean**

Retention: 180 days

Sink: Google BigQuery

We export the following logs regarding Glean Assistant usage to Glean which are scrubbed of PII:

* Timestamp
* Tracking tokens
* Scrubbed (anonymized) user ID
* Author type ("glean" or "user")
* Platform
* Initiator (Surface)
* Latency time
* Error and type
* Upvote or Downvote
* Manual Feedback message

Notably, we do not export to Glean any raw content of messages, response or any metadata from your company’s contents, or identifying user PII *except* when users click downvote on an answer.


!!! quote "How are the scrubbed/exported logs used?"

The purpose of the scrubbed exported logs are to measure:

* Daily Active Users (DAU)
* Engagement
* Retention
* Satisfaction
* Upvote / Downvote ratio
* Qualitatively analyze "bad" responses


!!! quote "How do we report issues to you so you can improve?"

Clicking downvote on an answer is the most effective way to report issues with Glean Assistant. By default, this sends us the raw text of the conversation history so engineers on our team can debug.

If you’d like a verbal response, please reach out to Glean Support, or to your Glean Customer Success Manager (CSM).


!!! quote "What controls do we have around data sent to the LLM?"
Exclusion rules under [Workplace settings > Assistant > Advanced > Exclusion rules](https://app.glean.com/admin/setup/gleanassistant?tab=advanced){:target="_blank"} allow you to exclude (red list) data from ever being sent to the LLM.

We provide 3 ways to red list data:

1. Specific documents via Document ID.
2. Specific folders/containers of content (e.g. channels in Slack, GDrive directories)
3. Specific datasources in their entirety (e.g. Slack, Jira)

:octicons-arrow-right-24: More information: [Excluding Content](){:target="_blank"}.


!!! quote "What controls do we have around the answers provided by Glean Assistant?"

Custom instructions under [Workplace settings > Assistant > Advanced > Advanced instructions](https://app.glean.com/admin/setup/gleanassistant?tab=advanced){:target="_blank"} allow you to control the answers that Glean Assistant provides to users. These are plaintext instructions that are applicable across the entire organizaiton, e.g.:

> Do not respond to any queries regarding salary.

> Do not respond if the query includes company financials.

:octicons-arrow-right-24: More information: [Custom Instructions](){:target="_blank"}.

---

## Customization

!!! quote "Can I use my own API Key?"

Yes, when GPT is selected as the LLM for Glean Assistant to use, you can opt to use your own OpenAI or Azure OpenAI key.

:octicons-arrow-right-24: More information: [Using Your Own Key](){:target="_blank"}.


!!! quote "How do I choose the LLM that Glean Assistant uses?"

As long as the LLM is on our list of [supported LLMs](){:target="_blank"}, you can contact Glean Support to switch to a specific LLM.


!!! quote "I want to use Google PaLM 2 as the LLM. How do I do this?"

Contact Glean Support to switch to a specific LLM.


!!! quote "Can I embed Glean Assistant & Glean Chat into our own internal applications? E.g. Our company intranet page?"

Yes! Many of our customer's have opted to do this; allowing them to re-brand Glean Chat under their brand. See our [Developer Documentation](https://developers.glean.com/docs/browser_api/chat/){:target="_blank"}; specifically the Web SDK for Chat.


!!! quote "Are there other ways I can use this? Slack? Teams?"
Yes!

If your organization uses Slack, you can configure Glean Assistant as a bot within your Slack workspace to automatically answer questions as employees post them.

The answers Glean Assistant provides are only visible to the employee who posted the message unless shared more broadly by them. Note, Glean Assistant will only be invoked if it has reasonable confidence that it can provide an accurate answer.

:octicons-arrow-right-24: More information: [Slackbot](){:target="_blank"}.

For Microsoft Teams, we are currently beta testing similar functionality.

We also offer an [API](https://developers.glean.com/docs/client_api/chat_api/){:target="_blank"} and [widget](https://developers.glean.com/docs/browser_api/chat/){:target="_blank"} that can be embedded into your existing internal apps.


!!! quote "Can we customize which datasources Glean Assistant has access to?"
Yes! This is achieved through content exclusions under [Workplace settings > Assistant > Advanced > Exclusion rules](https://app.glean.com/admin/setup/gleanassistant?tab=advanced){:target="_blank"}.

:octicons-arrow-right-24: More information: [Excluding Content](){:target="_blank"}.


!!! quote "Can we customize which set of users we want to roll this out to?"
Yes! Administrators can control this natively under [Workplace settings > Assistant > Setup > Early access users](https://app.glean.com/admin/setup/gleanassistant?tab=setup){:target="_blank"}


!!! quote "Can we provide a message to our users reminding them to verify the authenticity of generated content?"
Yes! This can be achieved with a custom instruction under [Workplace settings > Assistant > Advanced > Advanced instructions](https://app.glean.com/admin/setup/gleanassistant?tab=advanced){:target="_blank"}. For example:

> For every response, make sure you include a reminder that the answer may not be accurate.

:octicons-arrow-right-24: More information: [Custom Instructions](){:target="_blank"}.

---

## Developer

!!! quote "Do you provide API access to your Generative AI features?"

Yes! Please see our [Developer Documentation](https://developers.glean.com/docs/client_api/chat_api/){:target="_blank"} for Chat under our Client API.


!!! quote "Can I embed Glean Assistant & Glean Chat into our own internal applications? E.g. Our company intranet page?"

Yes! Many of our customer's have opted to do this; allowing them to re-brand Glean Chat under their brand. See our [Developer Documentation](https://developers.glean.com/docs/browser_api/chat/){:target="_blank"}; specifically the Web SDK for Chat.


!!! quote "Can we build our own applications and tools that leverage Glean Assistant as the LLM?"

Yes! This is achieved with our AI Apps Platform. Please contact your Glean Sales Team for more information.

---

## Support

!!! quote "The responses do not seem very good. Can they be improved?"

There are a few reasons that Glean Assistant may be providing lower-quality responses:

1. **Not enough datasources connected:** This is common in pilots and for new tenants. Glean Assistant completely depends on the information it has access to. We recommend onboarding ALL of your required datasources before enabling Glean Assistant.

2. **Low quality source material:** Glean Assistant can only be as good as the source material from which it generates responses from. If your material on a specific topic is limited or sparse, then Glean Assistant will also have trouble curating a response from it.

3. **M/L models not trained:** Also common in pilots and new tenants. Once all of your datasources have been connected, your Glean tenant will run multiple M/L workflows in the backend to enhance the quality of Glean Assistant responses. Sometimes these workflows do not run due to a threshold not being hit (i.e. not enough datasources connected yet). Contact Glean Support who can check this and initiate the workflows manually if you believe this to be the case.


!!! quote "How can we report poor quality responses to Glean?"

Clicking downvote on an answer is the most effective way to report issues with Glean Assistant. By default, this sends us the raw text of the conversation history so engineers on our team can debug.

If you’d like a verbal response, please raise a ticket with Glean Support, or reach out to your Glean Customer Success Manager (CSM).

