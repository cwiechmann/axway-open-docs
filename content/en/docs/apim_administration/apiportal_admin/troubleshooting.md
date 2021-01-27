---
title: Troubleshooting API Portal
linkTitle: Troubleshooting
weight: 110
date: 2019-07-30
description: General troubleshooting steps for API Portal, as well as specific
  problems and recommended solutions.
---
## General troubleshooting steps

1. Check if your issue and a workaround for it is listed as a known issue in the [Release Notes](/docs/apim_relnotes/) for your installed API Portal version.
2. Restart the failing servers or clients.
3. Collect the log files, screen shots, and any other data related to the issue, and contact Axway Support.

### Logging and error reporting

The Apache `error_log` file is located at `/var/log/apache2/`.

To enable Joomla! error reporting, in JAI, click **System > Global Configuration > Server** and set the error reporting to the desired level. However, use caution, because this may lead to warnings and errors on the API Portal pages. We recommended you to enable the error reporting only in critical situations, and not in a production environment.

For more information, see [Supported log files](/docs/apim_administration/apiportal_admin/apip_logging/).

## API response class details missing

The following is an example of missing response class details. An `array[null]` value is displayed instead of details:

![An example of an "array[null]" Response Class with missing details](/Images/APIPortal/troubleshooting1.png)

The following is an example of the expected response class details:

![An example showing an expected response class](/Images/APIPortal/troubleshooting2.png)

To solve this issue, set the correct return type for any APIs causing the error, and then republish them:

1. Log in to API Manager, and click **API Registration**.
2. Select the API causing the error, click **Manage selected**, and select **Unpublish**. You can unpublished multiple APIs at one go.
3. Click the API, select the **API Methods** tab, set **Response type** for the method causing the error, and click **Save**.
4. Go back to **API Registration**, select the edited API, click **Manage selected**, and select **Publish**.

## Random session logout

If you have the problem that the API-Portal keeps logging users out rather randomly, then it could be due to the session hijacking plugin running in the API-Portal.
It checks, for example, the `x-forwarded-for` HTTP header, which is typically set by an upstream reverse proxy, to see if it remains the same during a session. The port number also plays a role.  
An example would be:  
`89.211.212.232:50238`  
and then the port changes with the next request:  
`89.211.212.232:50239`  
If this happens, the user is logged out.  

So check if a reverse proxy is in use and if & how it sets the `X-Forwarded-For` header.
