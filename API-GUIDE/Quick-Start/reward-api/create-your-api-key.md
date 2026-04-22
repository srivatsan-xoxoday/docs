---
title: "Create Your API Key"
slug: "create-your-api-key"
excerpt: "Once you’ve received access to your sandbox or production account, follow these steps to generate your API key."
hidden: false
createdAt: "Wed Aug 06 2025 11:22:28 GMT+0000 (Coordinated Universal Time)"
updatedAt: "Tue Sep 02 2025 10:55:23 GMT+0000 (Coordinated Universal Time)"
---
All requests to the Xoxoday Rewards API must be authenticated.

Xoxoday uses bearer authentication, where each request must include an HTTP header that includes your Client ID, Secret ID, and Access Token. The following guide explains how to generate your client ID, secret ID, and access tokens from the admin portal.

## How to Generate Your API Key

1. Log in to your Xoxoday Admin Dashboard (Sandbox or Production).
2. Go to Settings → API.

<img src="https://files.readme.io/a66173533eadace1ff0e1a682e483d1bf113839925a551c2dca3871ffd245abc-Screenshot_2025-08-06_at_4.33.53_PM.png" align="left" width="40%" />
3. Under the Reward API tab, click Generate Client ID.

<img src="https://files.readme.io/80d03d78af63e1a2e8ce283fbc6bd6ea41cef808f8fd911923409827ace034f8-Screenshot_2025-08-17_at_4.42.34_PM.png" align="center" />
4. A pop-up will appear showing the scope of integration (Gift Card API). Click Save.

   Your Client ID and Secret ID will now be visible on the dashboard — copy and store them securely.

<img src="https://files.readme.io/2604e317b34c7bb1a81ca1c91403e526787591c664020691d8d6d9e0b07a73ed-Screenshot_2025-08-17_at_4.42.13_PM.png" align="left" />
5. Click on “Generate New Tokens”.

   ![](https://files.readme.io/c9342d005a457923658c5dd0fd254626825a116f85db4656be7c3ab349232d9d-Screenshot_2025-08-06_at_4.34.40_PM.png)
6. Confirm by clicking “Yes, Generate”.

<img src="https://files.readme.io/6aa35c341ee2122be9626e8ab0fcf2e3783301ea3949bbd930cfea7b7608af3c-Screenshot_2025-08-06_at_4.34.57_PM.png" align="left" width="60%" />
7. Your Access & Refresh Tokens will be displayed — copy it immediately, as it will not be shown again.

<img src="https://files.readme.io/1c5f0186a54dc5515322e917eed160324cb96c2edd8a0e9451b6221a3e25754b-Screenshot_2025-08-06_at_4.35.32_PM.png" align="left" width="50%" />

<br />

<br />

<br />

<br />

<br />

<br />

<br />

8. Treat this token like a password. Keep it secure and never expose it publicly.

## Using the API Key

To authenticate your API requests, include the access token in the Authorization header as a Bearer token:

```text
Authorization: Bearer <your-access-token>
```

This header is required for all authenticated API calls to both sandbox and production environments.

> Ensure that your token is kept secure and never exposed in client-side code or public repositories.