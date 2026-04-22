---
title: "Fetch Points API"
slug: "fetch-points-api"
excerpt: "This API endpoint allows you to fetch points for each user (which can be be displayed inside your UI)."
hidden: false
createdAt: "Thu Mar 14 2024 10:43:01 GMT+0000 (Coordinated Universal Time)"
updatedAt: "Mon Nov 24 2025 05:56:56 GMT+0000 (Coordinated Universal Time)"
openapi: "reward-points-spec.yaml POST /fetchPoints"
---
## Fetch Points API Schema

| **Property**      | **Type** | **Description**                       |
| :---------------- | :------- | :------------------------------------ |
| `user_data.email` | `String` | User’s email ID to fetch balance.     |
| `user_data.phone` | `String` | User’s phone number to fetch balance. |

## Response Schema

| **Path**                     | **Type**    | **Description**                                 |
| ---------------------------- | ----------- | ----------------------------------------------- |
| data                         | object      | Root response object.                           |
| data.user_balance            | object      | Container for user points/balance data.         |
| data.user_balance.success    | number      | API execution status (`1` = success).           |
| data.user_balance.message    | string/null | API message (null when no message is returned). |
| data.user_balance.data       | object      | Actual points data.                             |
| data.user_balance.data.total | number      | Total available reward points for the user.     |
