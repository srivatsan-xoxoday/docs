---
title: "Implementing Webhooks"
slug: "implementing-webhooks"
excerpt: ""
hidden: false
createdAt: "Sun Aug 10 2025 14:55:34 GMT+0000 (Coordinated Universal Time)"
updatedAt: "Tue Aug 19 2025 11:00:28 GMT+0000 (Coordinated Universal Time)"
---
Rewards APIs now support sending real-time callbacks to your pre-registered webhook URL for order delivery status updates.

### Event Supported

Currently, only the Order Delivery Status event is sent via webhook. The delivery status can be found in the `deliveryStatus` field of the webhook payload.

### Important

1. Whitelist Xoxoday’s callback IP – To ensure uninterrupted delivery of webhook notifications, whitelist:  
   `52.76.120.90`
2. Retry Policy – If a webhook POST fails, our system will retry up to three times. If all attempts fail, the webhook will be automatically disabled. You can re-enable it via the dashboard.

### Webhook Payload Example

```json
{  
  "id": \<Number(20)>,  
  "data": {  
    "orderId": \<Number(11)>,  
    "poNumber": \<String(100)>,  
    "orderDate": \<String(19)>,  
    "deliveryStatus": "\<delivered|canceled>"  
  },  
  "createdAt": \<String(19)>  
}
```

> Legend: \<DataType(size)>

### Payload Field Reference

| Parameter Name   | Type        | Description                                                                   |
| :--------------- | :---------- | :---------------------------------------------------------------------------- |
| `id`             | Integer(20) | Unique Webhook ID for identifying the callback event                          |
| `orderId`        | Integer(11) | Unique Xoxo Order ID generated when an order is placed via the Plum API       |
| `poNumber`       | String(100) | Purchase Order number provided by the client at the time of placing the order |
| `orderDate`      | String(19)  | Date and time when the order was placed                                       |
| `deliveryStatus` | String(9)   | Order delivery status – can be `delivered` or `canceled`                      |
| `createdAt`      | String(19)  | Date and time when the callback was sent                                      |
