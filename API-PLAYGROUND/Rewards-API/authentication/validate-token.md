---
title: "Validate Token"
slug: "validate-token"
excerpt: "One you've generated the access token, this article explains how you can validate the access token."
hidden: false
createdAt: "Tue Apr 04 2023 11:50:58 GMT+0000 (Coordinated Universal Time)"
updatedAt: "Mon Nov 24 2025 06:07:32 GMT+0000 (Coordinated Universal Time)"
openapi: "API-PLAYGROUND/Rewards-API/authentication/spec.yaml GET /token"
---
## Response Schema

| **Parameter**    | **Type** | **Description**                                                                               |
| ---------------- | -------- | --------------------------------------------------------------------------------------------- |
| **access_token** | string   | The validated access token issued by Xoxoday. Used for authorization in subsequent API calls. |
| **token_type**   | string   | Indicates the type of token. Always returned as `"bearer"`.                                   |
| **expires_in**   | number   | Epoch timestamp representing when the token will expire.                                      |

<br />

At any point, if you want to validate if the `access_token` is valid or not, then you can call the endpoint as outlined on this page.  The client application will pass the bearer token in the header.  The response to the request will be as outlined on the right-hand side panel.

> Note: `expires_in` is in seconds.
