---
title: "Refund API"
slug: "refund-api"
excerpt: "The RefundAPI allows clients to automate the refund process for their users. It ensures that points are credited back seamlessly without manual intervention. The API has to be built by the client so Xoxoday can consume it."
hidden: false
createdAt: "Fri Jul 21 2023 09:27:58 GMT+0000 (Coordinated Universal Time)"
updatedAt: "Tue Aug 26 2025 11:43:55 GMT+0000 (Coordinated Universal Time)"
---
## ⚠️ Important:

1. This API must be implemented and hosted by the client.
2. Xoxoday will consume this API to get the balance whenever required.
3. The request/response format below is provided only as a sample to illustrate the structure that Xoxoday expects.
4. Please ensure that your response is always in JSON format only, as our system does not support any other data types.

## Sample Request and Response

### Headers

1. `Content-Type: application/json`

### Sample Request

```json JSON (POST)
{
  "auth_token": "123xyz", 
  "unique_id": "22816281",
  "order_id": "AB1890082790",
  "redemption_amount": "200"
}
```

### Sample Request Schema

| Parameters        | Description                                                                                                                                         |
| ----------------- | --------------------------------------------------------------------------------------------------------------------------------------------------- |
| auth_token        | An authorisation value to successfully allow the request from Xoxoday to your system. This value is to be sent by the client during SSO redirection |
| unique_id         | Unique identifier of the user                                                                                                                       |
| order_id          | Order ID of the order                                                                                                                               |
| redemption_amount | Points/Amount used by the user                                                                                                                      |

### Sample Response Schema

```json
{
  "status": "1",
  "message": "Successfully updated",
  "data": {
    "order_id": "AB1890082790",
    "points": "200"
  }
}

```

### Sample Response Schema

| Parameters          | Description                         |
| ------------------- | ----------------------------------- |
| status              | 1 = Successful / 0 = Failure        |
| message             | Indicates the API's success/failure |
| data.transaction_id | Order ID of the voucher             |
| data.points         | Points refunded                     |

## Implementation Notes

1. Xoxoday will only consume this API — the client must build and expose it.
2. The `auth_token` must be provided by you under `tpd` object when SSO Redirection API is called . 
3. Make sure the API response includes accurate response status.

> Note: Refunds must be initiated against an existing Order ID. The refund amount cannot exceed the original order value associated with that Order ID.
