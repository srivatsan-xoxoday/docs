---
title: "Securing Webhooks"
slug: "securing-webhooks"
excerpt: ""
hidden: false
createdAt: "Sun Aug 10 2025 15:26:00 GMT+0000 (Coordinated Universal Time)"
updatedAt: "Tue Aug 19 2025 11:00:28 GMT+0000 (Coordinated Universal Time)"
---
To add an extra layer of security to your webhooks, we have introduced the x-API-key feature.  
When enabled, each webhook request will include a custom header (x-API-key) that you define.  
Your server can then validate this key to ensure the request came from us — preventing unauthorized systems from sending fake webhook payloads.

## How This Secures the Webhook

Without verification, anyone who knows your webhook URL could send fake requests that look real.  
By adding a secret x-API-key header:

1. We include the secret key in every webhook call we send to you.
2. You verify this key on your server before processing the payload.
3. Requests without the correct key (or with an incorrect one) are rejected.

This means that even if your webhook URL is exposed, malicious parties cannot successfully send data without knowing your secret key.

## How to Enable the Security Feature

1. Go to your Settings > API > Configure Webhook.
2. Toggle "Add Custom Header" to enable it.
3. In the x-API-key field, enter a secret key (alphanumeric, 13–60 characters).

   ![](https://files.readme.io/f87693e510ac2dd5eace9577b10acfed75146c2be249449423cdefe504fb4c97-image.png)
4. Click "Save Webhook" to save changes.

> From now on, all webhook payloads will include the x-API-key in the request header.

### Example x-api-key:

```json
x-api-key: a1p2z5b7v68b9112234
```

## How to Edit/Update the x-API-key

1. Click in the x-API-key field and update the value.
2. Click "Update Webhook" to save.
3. Future webhook calls will carry the new key.

## Webhook Payload Example

```json
Header:  
x-api-key: a1p2z5b7v68b9112234

Body:  
{  
    "id": \<Number(20)>,  
    "data": {  
        "orderId": \<Number(11)>,  
        "poNumber": \<String(100)>,  
        "orderDate": \<String(19)>,  
        "deliveryStatus": \<String(9)[Delivered|Canceled]>  
    },  
    "createdAt": \<String(19)>  
}  
```

> Legend  
> \<DataType(size)> → Data type and maximum size of the field.

## Parameters

| Parameter Name     | Type & Size    | Description                                  |
| :----------------- | :------------- | :------------------------------------------- |
| **x-api-key**      | String (13–60) | Secret header value to verify webhook source |
| **id**             | Integer (20)   | Unique webhook ID                            |
| **orderId**        | Integer (11)   | Unique Xoxo order ID                         |
| **poNumber**       | String (100)   | PO number (if provided at order time)        |
| **orderDate**      | String (19)    | Date/time when order was placed              |
| **deliveryStatus** | String (9)     | Status: `Delivered` or `Canceled`            |
| **createdAt**      | String (19)    | Timestamp when webhook was triggered         |
