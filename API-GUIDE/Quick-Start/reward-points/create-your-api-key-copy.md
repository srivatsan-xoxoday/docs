---
title: "Create Your API Key"
slug: "create-your-api-key-copy"
excerpt: "Once you’ve received access to your sandbox or production account, follow these steps to generate your API key."
hidden: false
createdAt: "Sun Aug 17 2025 11:32:55 GMT+0000 (Coordinated Universal Time)"
updatedAt: "Tue Aug 26 2025 14:22:33 GMT+0000 (Coordinated Universal Time)"
---
All requests to the Xoxoday Rewards API must be authenticated.

Xoxoday uses bearer authentication, where each request must include an HTTP header that includes your Client ID, Secret ID, and Access Token. The following guide explains how to generate your client ID, secret ID, and access tokens from the admin portal.

## How to Generate Your API Key

1. Log in to your Xoxoday Admin Dashboard (Sandbox or Production).
2. Go to Settings → API.
3. Under the Storefront Integration tab, click Generate New Tokens.
4. A pop-up will appear showing the scope of integration. Click Save.
5. Your Client ID and Secret ID will now be visible on the dashboard — copy and store them securely.
6. Click on “Generate New Tokens”.
7. Confirm by clicking “Yes, Generate”.
8. Your Access & Refresh Tokens will be displayed — copy it immediately, as it will not be shown again.
9. Treat this token like a password. Keep it secure and never expose it publicly.

## Using the API Key

To authenticate your API requests, include the access token in the Authorization header as a Bearer token:

```text
Authorization: Bearer <your-access-token>
```

This header is required for all authenticated API calls to both sandbox and production environments.

> Ensure that your token is kept secure and never exposed in client-side code or public repositories.