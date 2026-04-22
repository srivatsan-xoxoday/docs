---
title: "Send Points API"
slug: "send-points-api"
excerpt: "This document explains the API endpoint for Send Points"
hidden: false
createdAt: "Thu Mar 14 2024 14:15:20 GMT+0000 (Coordinated Universal Time)"
updatedAt: "Thu Jan 08 2026 10:46:43 GMT+0000 (Coordinated Universal Time)"
openapi: "reward-points-spec.yaml POST /sendPoints"
---
## Send Points API Schema

| **Property**                                      | **Type**      | **Description**                                         |
| :------------------------------------------------ | :------------ | :------------------------------------------------------ |
| `variables.recipients_data.sender_email`          | `String`      | **Super Admin email** sending the points.               |
| `variables.recipients_data.expiry_month`          | `Int/String`  | Expiry of points in month.                              |
| `variables.recipients_data.recipients`            | `[Recipient]` | List of recipient objects to whom balance will be sent. |
| `variables.recipients_data.recipients[].to_name`  | `String`      | Recipient’s full name.                                  |
| `variables.recipients_data.recipients[].to_email` | `String`      | Recipient’s email address.                              |
| `variables.recipients_data.recipients[].amount`   | `String`      | Amount of balance/credits to be sent.                   |
| `variables.recipients_data.recipients[].citation` | `String`      | Purpose or reference note for the transaction.          |

## Response Schema

| Property            | Type   | Description                                           |
| ------------------- | ------ | ----------------------------------------------------- |
| `data.unique_id`    | number | Unique identifier of the transaction.                 |
| `data.email`        | string | Email address of the recipient (optional).            |
| `data.points`       | number | Number of points to be credited or transferred.       |
| `data.name`         | string | Full name of the recipient user.                      |
| `data.phone_code`   | string | Country calling code of the recipient’s phone number. |
| `data.phone_number` | string | Mobile number of the recipient user.                  |
