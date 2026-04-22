---
title: "Get Payment Reports API"
slug: "get-payment-reports-api"
excerpt: "This API provides the payment history"
hidden: false
createdAt: "Mon Aug 25 2025 04:52:31 GMT+0000 (Coordinated Universal Time)"
updatedAt: "Mon Aug 25 2025 04:52:48 GMT+0000 (Coordinated Universal Time)"
openapi: "API-PLAYGROUND/Rewards-API/merchandise/spec.yaml POST /paymentHistory"
---
## Get Payment Report API Schema

| Parameter | Type    | Description                                  |
| :-------- | :------ | :------------------------------------------- |
| startDate | String  | the start date of the report                 |
| endDate   | String  | the end date to which the report is required |
| limit     | Integer | the number of entries that are required      |
| page      | Integer | define the pagination to extract the report  |

## Response

```json
{
  "data": {
    "h-0": "Parameter",
    "h-1": "Type",
    "h-2": "Description",
    "0-0": "invoice_number",
    "0-1": "Integer",
    "0-2": "This parameter provides the unique Invocie number  \nwhenever a Invoice is generated",
    "1-0": "reference_id",
    "1-1": "Integer",
    "1-2": "This parameter provides Order reference ID for any  \ndeductions or refunds",
    "2-0": "date",
    "2-1": "string",
    "2-2": "This parameter provides the transaction date",
    "3-0": "reason",
    "3-1": "string",
    "3-2": "This parameter provides the reason of the  \ntransaction like Funds added, Refunded, Brand  \nVoucher Issued",
    "4-0": "adjusted_amount",
    "4-1": "Integer",
    "4-2": "This parameter provides the information on amount  \nadded or deducted from the Balance",
    "5-0": "closing_balance",
    "5-1": "Integer",
    "5-2": "This parameter provides the information on the  \nclosing balance after every transaction",
    "6-0": "transaction_status",
    "6-1": "String",
    "6-2": "This provides information if the transaction status is  \neither Cancelled or Complete"
  },
  "cols": 3,
  "rows": 7,
  "align": [
    "left",
    "left",
    "left"
  ]
}
```
