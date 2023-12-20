---
icon: material/earth
title: "Supported GCP Regions"
description: The infrastructure required for a Glean deployment is not available in every GCP region. This document covers the supported GCP regions for Glean deployment.
authors:
  - Nathan Catania
sources:
  - https://docs.google.com/document/d/1HEGcjUZjhrSamFuSxsbHOyGroU0ut7TmG5sKAWEfrBg/edit
  - https://docs.google.com/spreadsheets/d/1THwN43trfMqwUggrslOKDxLrB3uDIJ536MnIQzwZCV8/edit#gid=921403900
---

This document covers the Google Cloud Platform (GCP) regions and zones validated and supported by Glean for tenant deployment; for both Glean hosted (SaaS) tenants, and cloud-prem (1) tenants.
{ .annotate }

1. Cloud-prem is when Glean builds your tenant within your own GCP project that is controlled by your organization.

Overall, there are two types of regions for hosting Glean: **Preferred** and **Non-Preferred** regions.

!!! info
    The default region for tenants hosted by Glean is `us-central-1`, which is located in North America. Please advise Glean if you would like your tenant deployed in an different region.


## Preferred Regions

Preferred regions are GCP regions that support the use of compatible [TPUs](https://cloud.google.com/tpu/docs/regions-zones) (1):
{ .annotate }

1. Tensor Processing Units (TPUs) are Google's custom-developed application-specific integrated circuits (ASICs) used to accelerate machine learning workloads. TPUs are more efficient and cost-effective than using GPUs for Machine Learning (M/L) workflows. More information: [Introduction to Cloud TPU (cloud.google.com)](https://cloud.google.com/tpu/docs/intro-to-tpu){:target="_blank"}.

| Region | Location                 | GCP Region     | GCP Zone         |
|--------|--------------------------|----------------|------------------|
| AMER   | USA (Iowa)               | `us-central1`  | `us-central1-a`  |
| APAC   | Taiwan (Changhua County) | `asia-east1`   | `asia-east1-c`   |
| EMEA   | Netherlands (Eemshaven)  | `europe-west4` | `europe-west4-a` |

Glean recommends that our customers leverage a Preferred Region for hosting their Glean tenant unless a specific country is required for data sovereignty purposes.

## Non-Preferred Regions

Non-Preferred regions are GCP regions that do not support TPUs.

In these regions Glean must use GPUs for M/L workflows, and these attract a higher usage cost due to a reduction in efficiency when compared to TPUs.

=== "Americas (AMER)"

    | Location                | GCP Region                | GCP Zone                      |
    |-------------------------|---------------------------|-------------------------------|
    | Brazil (Sao Paulo)      | `southamerica-northeast1` | `southamerica-northeast1-a,c` |
    | Canada (Montreal)       | `northamerica-northeast1` | `northamerica-northeast1-c`   |

=== "Asia Pacific (APAC)"

    | Location                | GCP Region                | GCP Zone                    |
    |-------------------------|---------------------------|-----------------------------|
    | Australia (Sydney)      | `australia-southeast1`    | `australia-southeast1-a,c`  |
    | India (Mumbai)          | `asia-south1`             | `asia-south1-a,b`           |
    | Japan (Tokyo)           | `asia-northeast1`         | `asia-northeast1-a`         |
    | Singapore (Jurong West) | `asia-southeast1`         | `asia-southeast-c,b,a`      |
    | South Korea (Seoul)     | `asia-northeast3`         | `asia-northeast3-b,a,c`     |

=== "Europe, the Middle East, and Africa (EMEA)"

    | Location                | GCP Region                | GCP Zone                    |
    |-------------------------|---------------------------|-----------------------------|
    | Belgium (St. Ghislain)  | `europe-west1`            | `europe-west1-b,c,d`        |
    | Germany (Frankfurt)     | `europe-west3`            | `europe-west3-b`            |
    | Israel (Tel Aviv)       | `me-west1`                | `me-west1-b,c`              |
    | Poland (Warsaw)         | `europe-central2`         | `europe-central2-b,c`       |
    | UK (London)             | `europe-west2`            | `europe-west2-a,b`          |

??? tip "Tip: Selecting a GCP Zone"
    Where possible, you should elect to use the first GCP zone referenced.
    
    The GCP zones above are listed in order of preference, that is: primary, secondary, tertiary. Some zones contain higher memory GPUs that are better suited for M/L workflows than others, and the order of the GCP zones listed above reflects the availability of the more efficient GPUs for that GCP region.
    
    For example: For Singapore, the listed GCP zone is `asia-southeast-c,b,a`. This means that while all 3 zones are technically supported, `asia-southeast-c` should be used over `asia-southeast-b`, which should be used over `asia-southeast-a`.

!!! warning
    Non-preferred regions attract an approximate 20-25% cost overhead compared to preferred regions due to the usage of GPUs over TPUs for M/L workflows.

    If you opt to use a non-preferred region:

    * **For Glean hosted tenants:** Your subscription cost will be higher to offset the higher infrastructure costs of these regions.
    * **For Cloud-prem tenants:** You should anticipate a 20-25% increase in monthly infrastructure costs for the Glean component of your GCP Billing Account.