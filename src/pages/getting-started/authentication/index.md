---
title: Authentication
description: Learn how to authenticate requests to Workfront Fusion APIs
keywords:
  - Workfront Fusion API Authentication
  - Server-to-Server Authentication
  - OAuth
  - API Security
  - Access Tokens
  - Client ID
  - Client Secret
  - Identity Management
  - Secure API Access
  - Token-Based Authentication
  - Generate Access Token
  - Authentication Best Practices
  - Fusion API
  - Workfront Automation
contributors:
  - 'https://github.com/annieTechno'
hideBreadcrumbNav: true
og:
  title: Authentication
  description: Learn how to authenticate requests to Workfront Fusion APIs
twitter:
  card: summary
  title: Authentication
  description: Learn how to authenticate requests to Workfront Fusion APIs
---

# Authentication

Learn how to authenticate requests to Workfront Fusion APIs

## Overview

Every request made to Workfront Fusion APIs must include an encrypted access token. Your secure, server-side application retrieves an access token by making a request to the [Adobe Identity Management System (IMS)](https://www.adobe.com/content/dam/cc/en/trust-center/ungated/whitepapers/corporate/adobe-identity-management-services-security-overview.pdf) with your **Client ID** and **Client Secret**.

## Prerequisites

This tutorial assumes you have worked with your Adobe Representative and have the following:

* An [Adobe Developer Console](https://developer.adobe.com/) account.
* A project with Adobe Fusion API [OAuth Server-to-Server credentials set up](https://developer.adobe.com/developer-console/docs/guides/services/services-add-api-oauth-s2s/). For more instructions on project creation, see [Create Credentials page](/workfront-fusion-apis/getting-started/credentials/).
* Access to your Client ID and Client Secret from the [Adobe Developer Console project](https://developer.adobe.com/developer-console/docs/guides/services/services-add-api-oauth-s2s/#api-overview). Securely store these credentials and never expose them in client-side or public code.

## Retrieve an access token

First, open a secure terminal and `export` your **Client ID** and **Client Secret** as environment variables so that your later commands can access them:

```bash
export FUSION_CLIENT_ID=<your_client_id>
export FUSION_CLIENT_SECRET=<your_client_secret>
```

Next, run the following command to generate an access token:

```bash
curl --location 'https://ims-na1.adobelogin.com/ims/token/v3' \
--header 'Content-Type: application/x-www-form-urlencoded' \
--data-urlencode 'grant_type=client_credentials' \
--data-urlencode "client_id=$FUSION_CLIENT_ID" \
--data-urlencode "client_secret=$FUSION_CLIENT_SECRET" \
--data-urlencode 'scope=openid,AdobeID,profile,additional_info.projectedProductContext'
```

The response will look like this:

```json
{"access_token":"yourExampleToken","token_type":"bearer","expires_in":86399}
```

Notice how the response includes an `expires_in` field, which informs you of how many more seconds the access token is valid for. Each access token is valid for 24 hours, after which your secure server-side application will need to request a new token. A best practice is to securely store the token and refresh it before it expires.

Export your access token as an environment variable:

```bash
export FUSION_ACCESS_TOKEN=yourExampleToken
```

Ready to put your API authentication to use? Continue to the [API Reference](/workfront-fusion-apis/api/) to explore available endpoints.
