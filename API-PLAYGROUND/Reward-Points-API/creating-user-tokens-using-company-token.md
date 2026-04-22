---
title: "Creating User Tokens using Company Token"
slug: "creating-user-tokens-using-company-token"
excerpt: ""
hidden: false
createdAt: "Thu Mar 14 2024 10:36:17 GMT+0000 (Coordinated Universal Time)"
updatedAt: "Mon Mar 23 2026 05:06:36 GMT+0000 (Coordinated Universal Time)"
openapi: "reward-points-spec.yaml POST /token/create/user"
---
## Creating user tokens API schema

| **Property** | **Type** | **Description**                                                   |
| :----------- | :------- | :---------------------------------------------------------------- |
| `user_input` | `String` | Super Admin email address.                                        |
| `scope`      | `String` | Permission scope being assigned/validated (e.g., `user_session`). |

## Response Schema

| **Path**             | **Type** | **Description**                                           |
| -------------------- | -------- | --------------------------------------------------------- |
| access_token         | string   | Newly generated access token for the user.                |
| token_type           | string   | Always `"bearer"`.                                        |
| expires_in           | number   | Token validity duration in seconds.                       |
| refresh_token        | string   | Token used to regenerate a new access token once expired. |
| access_token_expiry  | number   | Epoch timestamp (ms) when the access token expires.       |
| refresh_token_expiry | number   | Epoch timestamp (ms) when the refresh token expires.      |
