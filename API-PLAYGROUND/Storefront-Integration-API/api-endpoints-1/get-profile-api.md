---
title: "Get Profile API"
slug: "get-profile-api"
excerpt: "The Get Profile API is used to verify account information and prevent fraud at the time of checkout. This API provides a second layer of account verification before the reward is sent, ensuring a seamless and secure customer experience."
hidden: false
createdAt: "Fri Jul 21 2023 09:09:26 GMT+0000 (Coordinated Universal Time)"
updatedAt: "Tue Aug 26 2025 11:37:52 GMT+0000 (Coordinated Universal Time)"
---
## ⚠️ Important:

1. This API must be implemented and hosted by the client.
2. Xoxoday will consume this API whenever a redemption takes place.
3. The request and response below are provided only as a sample to illustrate the structure that Xoxoday expects.
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
    "message": "Successfully loaded user's data",
    "user_data": {
        "unique_id": "22816281",
        "company_email_id": "dwightschrute@dundlermifflin.com",
        "first_name": "Dwight",
        "last_name": "Schrute",
        "mobile_number": "+1-123456789"
    }
}
```

### Schema Response Schema

| Parameters                 | Description                   |
| -------------------------- | ----------------------------- |
| status                     | 1 = successful / 0 = failure  |
| user_data.unique_id        | Unique identifier of the user |
| user_data.company_email_id | Email address of the user     |
| user_data.first_name       | First name of the user        |
| user_data.last_name        | Last name of the user         |
| user_data.mobile_number    | Mobile number of the user     |

## Implementation Notes

1. Xoxoday will only consume this API — the client must build and expose it.
2. The `auth_token` must be provided by you under `tpd` object when SSO Redirection API is called . 
3. Make sure the API response includes accurate response status.
