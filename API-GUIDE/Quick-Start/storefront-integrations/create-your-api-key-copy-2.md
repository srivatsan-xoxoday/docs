---
title: "Create Your API Key"
slug: "create-your-api-key-copy-2"
excerpt: "Once you’ve received access to your sandbox or production account, follow these steps to generate your API key."
hidden: false
createdAt: "Tue Aug 26 2025 13:46:09 GMT+0000 (Coordinated Universal Time)"
updatedAt: "Tue Aug 26 2025 14:23:22 GMT+0000 (Coordinated Universal Time)"
---
All requests to the Xoxoday Rewards API must be authenticated.

Xoxoday uses bearer authentication, where each request must include an HTTP header that includes your Client ID, Secret ID, and Access Token. The following guide explains how to generate your client ID, secret ID, and access tokens from the admin portal.

## How to Generate Your API Key
## Generate API Tokens

1. Log in to your Xoxoday Admin Dashboard (Sandbox or Production).

2. Go to **Settings → API**.

   ![](https://files.readme.io/a66173533eadace1ff0e1a682e483d1bf113839925a551c2dca3873ffd245abc-Screenshot_2025-08-06_at_4.33.53_PM.png)

3. Under the **Storefront Integration** tab, click **Generate New Tokens**.

   ![](https://files.readme.io/d980b6cb30d7ffb207bd40d5a2fb941c2ccb64d8cff65ffec0a5de02f2ac4134-Screenshot_2025-08-25_at_12.58.56_PM.png)

4. A pop-up will appear showing the scope of integration. Click **Save**.

   ![](https://files.readme.io/16ad1ebf16754dcfa5ff8489a1022662a5a8c553662d25ab78820783771fb023-Screenshot_2025-08-25_at_12.59.13_PM.png)

5. Your **Client ID** and **Secret ID** will now be visible on the dashboard — copy and store them securely.

6. Click on **Generate New Tokens**.

   ![](https://files.readme.io/c569f48e9f3b1e610141d9e6646e3e47579106c09cf3f72f6eacb98607c0abcf-Screenshot_2025-08-25_at_1.25.51_PM.png)

7. Confirm by clicking **Yes, Generate**.

   ![](https://files.readme.io/6aa35c341ee2122be9626e8ab0fcf2e3783301ea3949bbd930cfea7b7608af3c-Screenshot_2025-08-06_at_4.34.57_PM.png)

8. Your **Access & Refresh Tokens** will be displayed — copy them immediately, as they will not be shown again.

   ![](https://files.readme.io/f94196897a16f592838fcb1ed0665e4c2addca901461db34c2507134460645dc-image.png)

9. Treat these tokens like a password. Keep them secure and never expose them publicly.

## Using the API Key

To authenticate your API requests, include the access token in the Authorization header as a Bearer token:

```text
Authorization: Bearer <your-access-token>
```

This header is required for all authenticated API calls to both sandbox and production environments.

> Ensure that your token is kept secure and never exposed in client-side code or public repositories.
