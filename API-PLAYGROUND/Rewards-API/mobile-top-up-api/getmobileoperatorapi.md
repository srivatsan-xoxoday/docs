---
title: "Get Mobile Operator API"
slug: "getmobileoperatorapi"
excerpt: "Returns the mobile operator details for a given mobile number to enable accurate operator selection before placing a top-up order."
hidden: false
createdAt: "Thu Jan 22 2026 06:13:53 GMT+0000 (Coordinated Universal Time)"
updatedAt: "Thu Feb 19 2026 11:58:31 GMT+0000 (Coordinated Universal Time)"
openapi: "API-PLAYGROUND/Rewards-API/mobile-top-up-api/spec.yaml POST /getMobileOperator"
---
## Request Schema

| Data Type | Description                                        |
| --------- | -------------------------------------------------- |
| String    | Mobile number in E.164 format for operator lookup. |

## Response Schema

| Parameter          | Data Type | Description                                                              |
| ------------------ | --------- | ------------------------------------------------------------------------ |
| `status`           | String    | Indicates the result of the lookup request (e.g., `success`, `failure`). |
| `message`          | String    | Message describing the lookup result.                                    |
| `phone`            | String    | Mobile number in E.164 format that was validated.                        |
| `network_operator` | String    | Operator identified for the given mobile number.                         |
| `is_active`        | Boolean   | Indicates whether the mobile number is active.                           |
| `parentProductId`  | Integer   | Internal product ID mapped to the identified mobile operator.            |

> Note: You can use the same parentProductId in the Get Mobile Top-Up Catalogue API to fetch plans specific to the identified operator.
