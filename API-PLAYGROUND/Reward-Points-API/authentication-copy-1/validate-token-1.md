---
title: "Validate Token"
slug: "validate-token-1"
excerpt: "One you've generated the access token, this article explains how you can validate the access token."
hidden: false
createdAt: "Mon Aug 25 2025 08:42:02 GMT+0000 (Coordinated Universal Time)"
updatedAt: "Mon Nov 24 2025 06:08:55 GMT+0000 (Coordinated Universal Time)"
openapi: "reward-points-spec.yaml GET /token"
---
At any point, if you want to validate if the `access_token` is valid or not, then you can call the endpoint as outlined on this page.  The client application will pass the bearer token in the header.  The response to the request will be as outlined on the right-hand side panel.

## Response Schema

| **Property**         | **Type** | **Description**                                           |
| -------------------- | -------- | --------------------------------------------------------- |
| access_token         | string   | Newly generated access token for authenticated API calls. |
| token_type           | string   | Always `"bearer"`.                                        |
| expires_in           | number   | Token validity duration in seconds.                       |
| access_token_expiry  | number   | Epoch timestamp (ms) when the access token will expire.   |
| refresh_token_expiry | number   | Epoch timestamp (ms) when the refresh token will expire.  |
