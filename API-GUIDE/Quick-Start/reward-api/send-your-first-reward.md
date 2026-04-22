```mdx
---
title: "Send Your First Reward"
slug: "send-your-first-reward"
excerpt: "Here’s how to place your first reward order."
hidden: false
createdAt: "Wed Aug 06 2025 11:59:09 GMT+0000 (Coordinated Universal Time)"
updatedAt: "Fri Oct 24 2025 07:24:28 GMT+0000 (Coordinated Universal Time)"
---
Let’s send ourselves a test USD 50 reward

Run the cURL command below, replacing both <YOUR-ACCESS-TOKEN> and <YOUR-EMAIL-ADDRESS> with your own details:

```curl
curl --location 'https://stagingstores.xoxoday.com/chef/v1/oauth/api' \
--header 'Authorization: Bearer <your-access-token>' \
--header 'Content-Type: application/json' \
--data-raw '{
  "query": "plumProAPI.mutation.placeOrder",
  "tag": "plumProAPI",
  "variables": { 
    "data": {
      "productId": "55395",
      "quantity": "1",
      "denomination": "50",
      "poNumber": "",
      "email": "youremail@example.com",
      "contact": " ",
      "tag": "",
      "notifyReceiverEmail": 1
    }
  }
}'
```

### Response

If your request is successful, you’ll receive a JSON response like the one below with your voucher details.Check your inbox — your demo reward has just landed: 

```json
{
    "data": {
        "placeOrder": {
            "status": 1,
            "data": {
                "orderId": 6552967,
                "orderTotal": 8.79,
                "rawOrderTotal": 8.7917,
                "orderDiscount": "",
                "rawOrderDiscount": "",
                "discountPercent": "0",
                "currencyCode": "INR",
                "currencyValue": 1,
                "amountCharged": 8.79,
                "orderStatus": "complete",
                "deliveryStatus": "delivered",
                "tag": "Hello",
                "quantity": 1,
                "vouchers": [
                    {
                        "productId": 55395,
                        "orderId": 6552967,
                        "voucherCode": "https://stagingstores.plum.gift/3YEyDBWOeuYnyzpD",
                        "pin": "",
                        "validity": "2026-08-19",
                        "amount": 50,
                        "currency": "CRC",
                        "country": "IN,US",
                        "type": "url",
                        "currencyValue": 5.68716121
                    }
                ],
                "voucherDetails": [
                    {
                        "orderId": 6552967,
                        "productId": 55395,
                        "productName": "Amazon USA - ZENDIT",
                        "currencyCode": "USD",
                        "productStatus": "delivered",
                        "denomination": 50,
                        "vendorLogo": ""
                    }
                ],
                "orderMeta": {
                    "email": "rishabh.kumar@xoxoday.com",
                    "contact": "+91-8168147851"
                }
            }
        }
    }
}
```

### Check Your Inbox

You’ve just received a reward sent via the Xoxoday API. Congratulations — you’ve officially placed your first reward.

```block:image
{
  "images": [
    {
      "image": [
        "https://files.readme.io/768a0dc7d99c6e34749cb85e76435d09456251c5030b8508e2dc34b0b66807a7-image.png",
        null,
        ""
      ],
      "align": "center",
      "sizing": "60% "
    }
  ]
}
```
```