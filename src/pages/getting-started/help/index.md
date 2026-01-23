---
title: Create Credentials - Workfront Fusion API
description: This guide explains how to create credentials for the Workfront Fusion API.
keywords:
  - Workfront Fusion API
  - Fusion API Authentication
  - automation API
  - integration platform
  - workflow automation
  - REST API
  - enterprise automation
  - system integration
  - Workfront Fusion Services
  - Create Credentials
  - Credentials
  - OAuth Server-to-Server
contributors:
  - 'https://github.com/annieTechno'
hideBreadcrumbNav: true
og:
  title: Create Credentials - Workfront Fusion API
  description: This guide explains how to create credentials for the Workfront Fusion API.
twitter:
  card: summary
  title: Create Credentials - Workfront Fusion API
  description: This guide explains how to create credentials for the Workfront Fusion API.
---

# Get Credentials

<InlineAlert variant="info" slots="text" />

This page contains instructions for **IMS organization admins  only** to create project credentials for their teams. If you are a developer and your admin has shared a valid key with you, head over to the [quickstart guide](../index.md)

## Access Adobe Developer Console

Navigate to the __API and services__ section. Search for __Workfront Fusion API__.

![API and services page - Fusion API card](./devconsole.png)

Can't find the Workfront Fusion API? Make sure you are accessing from the organization that has Fusion product license. 

## Create a new project

Once you can see the Fusion API product card, click the __Create project__ button.

1. Let's start by registering your project name. This will help you find your project in the Developer Console later. You will be able to modify this name later.
2. Click on __Save configured API__ in the following modal. On the next screen, you will be able to see your __client ID__ (API key).
3. From the left navigation, select __OAuth Server-to-Server__ and you can click __Retrieve client secret__ to get your client secret.

__To make calls to the Fusion API, developer(s) need a valid client ID (API key) and an access token__. Since organization admins are the only ones who can access these projects in the Console, using the __Generate access token__ button on the credential overview page is not ideal.

<InlineAlert variant="info" slots="text" />

Instead of sharing access tokens, we recommend sharing the __client ID__ and __client secret__ with developers who need access to the API. This way, they can programmatically generate new access tokens as each access token expires after 24 hours.

## Share credentials with developers

After you have successfully configured your project in Developer Console:

- In the __Generate access tokens__ block, select __View cURL command__.
- Copy the command and share with developers in your org. It should look similar to the following:

```bash
curl -X POST 'https://ims-na1.adobelogin.com/ims/token/v3' \
-H 'Content-Type: application/x-www-form-urlencoded' \
-d 'grant_type=client_credentials&client_id={client_id}&client_secret={client_secret}&scope=openid,AdobeID,profile,additional_info.projectedProductContext'
```

Read more about generating access tokens in the [authentication guide](../index.md). 

## Next steps

Once your developers have their credentials, they can:

- Follow the [authentication guide](../index.md) to generate access tokens
- Explore the [API Reference](../../api/index.md) to discover available endpoints
- Build automations using the Fusion API to manage scenarios, connections, hooks, and executions

<InlineAlert variant="info" slots="text" />
To manage technical account permissions and assign them to specific Fusion teams, refer to the [Technical Accounts￼ guide](../technical_accounts/index.md).
