---
title: Use Traceability Agent to report Gateway usage
linkTitle: Use Traceability Agent to report Gateway usage
draft: false
weight: 10
description: Understand how the Traceability Agent reports the Gateway usage to Amplify platform.
---
## Before you start

* Make sure your entitlement is correctly set up, based on your Gateway (AWS / Axway v7 / Azure). Refer to your Axway CSM for more information.

## Objectives

Learn how to install and set up the Traceability Agent to automatically report the Gateway usage data to Amplify platform. Gateway usage data counts all API calls going through the Gateway.

## Traceability Agent overview

The Traceability Agent is attached to a Gateway and monitors the traffic crossing it. The collected traffic is reported to Amplify platform in different event:

* **Usage** event: report the total number of API calls during a period of time. This feature cannot be inactivated.
* **Transaction** event: report the transaction summary (API name, duration, status), as well as the transaction details (request/response headers from the frontend and backend of the API). This feature can be inactivated be either using the environment variable `CENTRAL_PUBLISHTRAFFIC=false`, or you can reduce the number of transaction sent to the platform using the [sampling feature](/docs/central/connected_agent_common_reference/trace_sampling).

## Network pre-requisites

All outbound traffic is sent over SSL via TCP / UDP.

Open the following ports so that agents can communicate to the Amplify platform:

| Region | Host                                                                                      | IP             | port       | Protocol     | data                               |
|--------|-------------------------------------------------------------------------------------------|----------------|------------|--------------|------------------------------------|
|        |                                                                                           |                |            |              |                                    |
| EU/US  | login.axway.com                                                                           | 52.58.132.2    | 443        | HTTPS        | Platform authentication |
|        |                                                                                           | 52.29.4.35     |            |              |                                    |
|        |                                                                                           | 54.93.140.145  |            |              |                                    |
|        |                                                                                           |                |            |              |                                    |
| US     | apicentral.axway.com                                                                      | 3.94.245.118   | 443        | HTTPS        | API definitions, Subscription info |
|        |                                                                                           | 54.208.199.251 |            |              |                                    |
|        |                                                                                           | 3.212.78.217   |            |              |                                    |
|        |                                                                                           | 52.202.95.208  |            |              |                                    |
|        |                                                                                           | 107.23.176.64  |            |              |                                    |
|        |                                                                                           | 3.225.16.120   |            |              |                                    |
|        |                                                                                           |                |            |              |                                    |
| EU     | central.eu-fr.axway.com                                                                   | 52.47.84.198   | 443        | HTTPS        | API definitions, Subscription info |
|        |                                                                                           | 13.36.25.69    |            |              |                                    |
|        |                                                                                           | 35.181.21.87   |            |              |                                    |
|        |                                                                                           | 13.36.2.143    |            |              |                                    |
|        |                                                                                           | 13.36.52.216   |            |              |                                    |
|        |                                                                                           | 15.236.7.112   |            |              |                                    |
|        |                                                                                           |                |            |              |                                    |
| EU/US  | lighthouse.admin.axway.com                                                                |                | 443        | HTTPS        | API usage event                  |
|        |                                                                                           |                |            |              |                                    |
| US     | ingestion-lumberjack.datasearch.axway.com or ingestion.datasearch.axway.com               | 54.225.171.111 | 453 or 443 | TCP or HTTPS | API transaction event                     |
|        |                                                                                           | 54.225.2.221   |            |              |                                    |
|        |                                                                                           | 54.146.97.250  |            |              |                                    |
|        |                                                                                           | 54.147.98.128  |            |              |                                    |
|        |                                                                                           | 52.206.193.184 |            |              |                                    |
|        |                                                                                           | 54.225.92.97   |            |              |                                    |
|        |                                                                                           |                |            |              |                                    |
| EU     | ingestion-lumberjack.visibility.eu-fr.axway.com  or  ingestion.visibility.eu-fr.axway.com | 15.236.125.123 | 453 or 443 | TCP or HTTPS | API transaction event                     |
|        |                                                                                           | 35.180.77.202  |            |              |                                    |
|        |                                                                                           | 13.36.27.97    |            |              |                                    |
|        |                                                                                           | 13.36.33.229   |            |              |                                    |

{{% alert title="Note" %}}
_Region_ column represents the region where your Amplify organization is deployed. EU means deployed in European data center and US meaning deployed in US data center. You must use the corresponding _Host_/_Port_ for your agents to operate correctly.
{{% /alert %}}

## Install Traceability Agent

To report usage to Amplify platform, the traceability Agent must be installed and connected to the Gateway to be monitored:

1. Install Axway CLI and Axway Central CLI

   * Install Axway CLI: `npm install -g axway`.
   * Install Axway Central CLI: `axway pm install @axway/axway-central-cli`.
   * Download and install OpenSSL, if not already present on the machine. This will help you generate a public/private key pair to secure the connection between Traceability Agent and Amplify platform.

      More information regarding the CLI installation is available [here](/docs/central/cli_central/cli_install/)

2. Authorize your CLI to use the Amplify Central APIs: `axway auth login`.

3. Install the Traceability Agent using Axway Central CLI: `axway central install agents`:

   * For usage tracking, only the Traceability Agent is required.
   * Answer ALL questions when prompted (environment / team / connectivity with Gateway).
   * CLI creates appropriate resources in Amplify platform / local files based on the answers.
   * CLI output next steps: copy files on the Gateway machine / start the agent.

      For more information regarding agents installation, see [Axway Gateway agents](/docs/central/connect-api-manager/deploy-your-agents-with-amplify-cli), [AWS Gateway agents](/docs/central/connect-aws-gateway/deploy-your-agents-with-amplify-cli), [Azure Gateway agent](/docs/central/connect-azure-gateway/deploy-your-agents-with-amplify-cli).

## Reporting Gateway usage event

You can view the environment in **Amplify Central > Topology** once the Traceability Agent is installed. The same environment is visible in Amplify platform under the **Organization** menu.

Once Traceability Agent starts, it detects the Gateway traffic, and begins counting the transactions. On a regular basis (default is 15 minutes), the Traceability Agent sends the usage counter to the platform.

To change the reporting interval, use the `CENTRAL_EVENTAGGREGATIONINTERVAL` variable with either a second, minute or hour notation:

```shell
# report every 5 minutes expressed in second unit
CENTRAL_EVENTAGGREGATIONINTERVAL=900s

# report every 5 minutes expressed in minute unit
CENTRAL_EVENTAGGREGATIONINTERVAL=15m

# report every hour expressed in hour unit
CENTRAL_EVENTAGGREGATIONINTERVAL=1h
```

If for any reason the usage report cannot be uploaded to Amplify platform, the data are kept in memory and will be pushed at the next trigger interval.

If the Traceability Agent is stopped while there are still remaining usage events to be sent, the report is saved on the disk where the Traceability Agent is located. The data will be sent to Amplify platform at the next Traceability Agent startup.

## View the usage data from Amplify platform

Based on the frequency you choose, the Traceability Agent reports to the platform the number of transactions that happen during each period. To view the data:

* Log into the platform, select the **Organization** menu:

![Usage data menu](/Images/central/connected_agent_common_reference/organization_menu.png)

* Select the **Usage** menu to view the usage data:

![Usage data menu](/Images/central/connected_agent_common_reference/usage_data_menu.png)

* Select a Usage data report tab:

    * **Monthly Usage** to visualize your monthly data. Filter either by month (to get a specific month's values), or products (if you have multiple product entitlements).
    * **Report History** to view and download the usage report history. Filter the data per reporting period and/or per file name, environment name or status.

![Usage report page](/Images/central/connected_agent_common_reference/usage_report_screen.png)

* Click **Download** to download a specific report.

## Known limitations

The following known limitations exist in the current implementation.

{{% alert title="Note" %}}
The usage report is based on the transactions the Traceability Agent monitors. If the transactions are not provided by the Gateway, the usage report will be inaccurate.
{{% /alert %}}

### Axway API Gateway

In the case of high demand, Axway recommends to turn off the trace event logging of the Gateway. In this situation, the Traceability Agent will not be able to monitor the transactions or report the corresponding traffic.

### AWS API Gateway

The current solution relies on AWS Simple Queue Service to collect traffic from Cloud Watch. However, there is a limit of 10 SQS messages per client connection that can be consumed at one time. As a workaround, you can increase the number of workers (i.e., consumer clients) using the `AWS_WORKERS` variable. Be aware that the number of workers is directly related to the network consumption -- the more you add, the more network connections are used.

### Azure API Gateway

Within Azure API Gateway, it is possible to activate the transaction sampling for Azure Monitoring (either at API level or for all APIs). Activating sampling will make the usage report inaccurate.
