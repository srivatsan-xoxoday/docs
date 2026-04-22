---
title: "Create Your API Key"
slug: "create-your-api-key-copy-1"
excerpt: "Once you’ve received access to your sandbox or production account, follow these steps to generate your API key."
hidden: false
createdAt: "Sun Aug 17 2025 17:39:39 GMT+0000 (Coordinated Universal Time)"
updatedAt: "Tue Sep 02 2025 10:55:42 GMT+0000 (Coordinated Universal Time)"
---
All requests to the Xoxoday Rewards API must be authenticated.

Xoxoday uses bearer authentication, where each request must include an HTTP header that includes your Client ID, Secret ID, and Access Token. The following guide explains how to generate your client ID, secret ID, and access tokens from the admin portal.

## How to Generate Your API Key

1. Log in to your Xoxoday Admin Dashboard (Sandbox or Production).
2. Go to Settings → API.

3. Under the Reward API tab, click Generate Client ID.

4. A pop-up will appear showing the scope of integration (Plum PRO API/Gift Card API). Click Save.

   Your Client ID and Secret ID will now be visible on the dashboard — copy and store them securely.

5. Click on “Generate New Tokens”.
6. Confirm by clicking “Yes, Generate”.
7. Your Access & Refresh Tokens will be displayed — copy it immediately, as it will not be shown again.

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