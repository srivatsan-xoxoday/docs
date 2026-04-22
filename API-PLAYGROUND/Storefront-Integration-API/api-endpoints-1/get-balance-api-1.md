---
title: "Get Balance API"
slug: "get-balance-api-1"
excerpt: "After a successful SSO redirection, Xoxoday will call the client’s Point Balance API to fetch the end user’s available points."
hidden: false
createdAt: "Fri Jul 21 2023 08:37:46 GMT+0000 (Coordinated Universal Time)"
updatedAt: "Tue Aug 26 2025 11:32:47 GMT+0000 (Coordinated Universal Time)"
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
"unique_id":"DB123",
"auth_token":"asdgfjhbsdlkjbasdlkjbadslkbdakasdhfjhfdb=="
}
```

### Sample Request Schema

| Parameter    | Type   | Description                                                                                       |
| ------------ | ------ | ------------------------------------------------------------------------------------------------- |
| `unique_id`  | String | Unique identifier of a user (sent by Xoxoday in the SSO redirection request).                     |
| `auth_token` | String | Authorization value provided by the client during SSO redirection. Used by Xoxoday for API calls. |

### Sample Response

```json
{
  "status": 1,
  "data": {
    "unique_id": "DB123",
    "points": "400"
  }
}
```

### Sample Response Schema

| Parameters | Description                 |
| ---------- | --------------------------- |
| status     | 1 = success / 0 = failure   |
| unique_id  | Unique identifier of a user |
| points     | Current points of a user    |

## Implementation Notes

1. Xoxoday will only consume this API — the client must build and expose it.
2. The `auth_token` must be provided by you under `tpd` object when SSO Redirection API is called . 
3. Make sure the API response includes accurate response status.
