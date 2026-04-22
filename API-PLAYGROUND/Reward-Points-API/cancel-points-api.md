---
title: "Cancel Points API"
slug: "cancel-points-api"
excerpt: "This API allows you to cancel previously issued points for one or more recipients using their unique identifier."
hidden: false
createdAt: "Thu Jan 08 2026 10:52:45 GMT+0000 (Coordinated Universal Time)"
updatedAt: "Thu Jan 22 2026 09:08:00 GMT+0000 (Coordinated Universal Time)"
openapi: "reward-points-spec.yaml POST /cancelPoints"
---
## Request Schema

| Property                                 | Type   | Description                                                              |
| ---------------------------------------- | ------ | ------------------------------------------------------------------------ |
| `recipients_data.recipients`             | array  | List of recipients for whom points cancellation is requested.            |
| `recipients_data.recipients[].unique_id` | number | Unique transaction ID of the points issuance that needs to be cancelled. |

## Response Schema

| Property                                    | Type    | Description                                                                  |
| ------------------------------------------- | ------- | ---------------------------------------------------------------------------- |
| `data.cancelBalance.error`                  | boolean | Indicates whether the cancellation operation failed (`false` = success).     |
| `data.cancelBalance.message`                | string  | Summary message describing the overall cancellation result.                  |
| `data.cancelBalance.recipients`             | array   | List of point transactions processed in the cancellation request.            |
| `data.cancelBalance.recipients[].unique_id` | number  | **Unique transaction ID** of the points issuance.                            |
| `data.cancelBalance.recipients[].success`   | boolean | Indicates whether the transaction cancellation was successful.               |
| `data.cancelBalance.recipients[].message`   | string  | Transaction-level status message explaining the outcome of the cancellation. |
