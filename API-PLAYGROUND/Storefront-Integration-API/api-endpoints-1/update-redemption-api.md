---
title: "Update Redemption API"
slug: "update-redemption-api"
excerpt: "The Update Redemption Transaction API allows Xoxoday to post redemption information to the client’s system whenever a user redeems points."
hidden: false
createdAt: "Fri Jul 21 2023 08:37:51 GMT+0000 (Coordinated Universal Time)"
updatedAt: "Tue Aug 26 2025 11:11:13 GMT+0000 (Coordinated Universal Time)"
---
## ⚠️ Important:

1. This API must be implemented and hosted by the client.
2. Xoxoday will consume this API whenever a redemption takes place.
3. The request and response below are provided only as a sample to illustrate the structure that Xoxoday expects.
4. Please ensure that your response is always in JSON format only, as our system does not support any other data types.

## Sample Request and Response

### Headers

1. application/JSON

### Sample Request

```json JSON (POST)
{
  "unique_id": "TTEO32S99ERCL",
  "auth_token": "0fe121f67cb0b90ef39fd83380bf1e12310912c86f4d7d5bfed3f3198e531b4f8d8af179b68361da28d0bc0353ce45ac7c374aa9c51dfb54c6705571f5ab8fe8",
  "total_points_redeemed": 348.5,
  "order_id": "AB1890082790",
  "order_date": 1693995688,
  "orderData": [
    {
      "quantity": 1,
      "orderAmount": 10,
      "product": {
        "productId": "28811",
        "name": "Sony MDR-ZX110AP Wired On-Ear Headphones with tangle free cable",
        "category": "merchandise",
        "price": 10
      }
    },
    {
      "quantity": 1,
      "orderAmount": 337.5,
      "product": {
        "productId": "28628",
        "name": "Flipkart Rs.250 Gift Card",
        "category": "giftcard",
        "price": 337.5
      }
    }
  ]
}

```

### Sample Request Schema

| Parameter               | Type                   | Requirement | Description                                                                                          |
| ----------------------- | ---------------------- | ----------- | ---------------------------------------------------------------------------------------------------- |
| `unique_id`             | String (email / phone) | Required    | Unique identifier for the user so that points are updated to the correct account.                    |
| `auth_token`            | String                 | Required    | Authorization value to allow the request from Xoxoday. Can be hash, Basic Auth, Bearer token, etc.   |
| `total_points_redeemed` | Integer / Float        | Required    | Total number of redeemed points.                                                                     |
| `order_id`              | String / Integer       | Required    | Unique Order ID that helps track the transaction.                                                    |
| `order_date`            | Integer (epoch)        | Optional    | Epoch timestamp of when the order was placed.                                                        |
| `orderData`             | Array                  | Optional    | List of redeemed items, with product details (ID, name, category, price, quantity, and orderAmount). |
| `orderData[].product`   | Object                 | Optional    | Contains details of the product being redeemed.                                                      |

### Sample Response

```json
{
  "status": "1",
  "message": "Successfully updated",
  "data": {
    "order_id": "12345"
  }
}
```

### Sample Response Schema

| Parameters | Description                                 |
| ---------- | ------------------------------------------- |
| status     | 1 = success / 0 = failure                   |
| message    | Indicates the APIs success/failure          |
| order_id   | Order ID of the item(s) ordered by the user |

## Implementation Notes

1. Xoxoday will only consume this API — the client must build and expose it.
2. The `auth_token` must be provided by you under `tpd`object  when SSO Redirection API is called . 
3. Make sure the API response includes accurate response status.
