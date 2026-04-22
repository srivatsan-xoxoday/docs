---
title: "Get Balance API"
slug: "getbalance"
excerpt: "Balance API allows you to fetch the available balance in your Admin wallet"
hidden: false
createdAt: "Wed Nov 12 2025 12:48:09 GMT+0000 (Coordinated Universal Time)"
updatedAt: "Wed Feb 04 2026 19:38:19 GMT+0000 (Coordinated Universal Time)"
openapi: "API-PLAYGROUND/Rewards-API/airmiles-api/spec.yaml POST /getBalance"
---
## Response Schema

| **Path**                      | **Type** | **Description**                             |
| ----------------------------- | -------- | ------------------------------------------- |
| data                          | object   | Root response object.                       |
| data.getBalance               | object   | Container for balance details.              |
| data.getBalance.status        | number   | API execution status (`1` = success).       |
| data.getBalance.data          | object   | Balance information object.                 |
| data.getBalance.data.value    | number   | Available balance value.                    |
| data.getBalance.data.currency | string   | Currency code of the balance (e.g., `USD`). |

> Note  
> Rather than fetching the balance before every order, you can use the Low Balance Notification option in the Admin Dashboard to receive alerts when the balance reaches the set threshold. [Click here to know more.](https://app.supademo.com/demo/cm9i4wxn923rmljv5hap9e5ic)
