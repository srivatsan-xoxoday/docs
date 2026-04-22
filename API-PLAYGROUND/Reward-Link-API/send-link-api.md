---
title: "Send Link API"
slug: "send-link-api"
excerpt: "The Send Link API generates a unique reward link for an email address and delivers it to the user’s inbox. It is ideal for automating reward distribution and notifications."
hidden: false
createdAt: "Fri Apr 07 2023 06:54:05 GMT+0000 (Coordinated Universal Time)"
updatedAt: "Mon Nov 24 2025 06:02:05 GMT+0000 (Coordinated Universal Time)"
openapi: "reward-link-spec.yaml POST /sendLinks"    
---
## Send Link API

| **Property**  | **Type** | **Description**                                                        |
| :------------ | :------- | :--------------------------------------------------------------------- |
| `campaignId`  | `String` | Unique identifier of the campaign for which links are to be generated. |
| `email_ids`   | `String` | Comma-separated list of recipient email addresses (or a single email). |
| `link_expiry` | `String` | Expiry date for the link(s) (format: `DD-MM-YYYY`).                    |

## Response Schema

| **Property**              | **Type** | **Description**                                                   |
| ------------------------- | -------- | ----------------------------------------------------------------- |
| data                      | object   | Root response object.                                             |
| data.generateLink         | object   | Container for link-sending operation.                             |
| data.generateLink.success | number   | API execution status (`1` = success).                             |
| data.generateLink.message | string   | Message returned by the API (e.g., “Links created successfully”). |
