---
title: "Place Order API"
slug: "place-airmiles-order"
excerpt: "With Place Order API, you can place orders of Airmiles available in the Catalog."
hidden: false
createdAt: "Wed Nov 12 2025 12:48:13 GMT+0000 (Coordinated Universal Time)"
updatedAt: "Wed Feb 04 2026 19:38:55 GMT+0000 (Coordinated Universal Time)"
openapi: "API-PLAYGROUND/Rewards-API/airmiles-api/spec.yaml POST /placeOrder"
---
> A unique reference ID needs to be sent for every unique order in the "poNumber" parameter
>
> We strongly recommend storing the request and response of every "PlaceOrderAPI" call

## Implementation Notes

1. To avoid facing an error while placing an order, please pass the valid productID and denomination
2. The maximum order quantity allowed for the products is 1 as mentioned  in the **"orderQuantityLimit"** parameter in the GetVouchersAPI
3. Should you wish to notify the recipient via email, please pass "1" in the **"notifyReceiverEmail"** parameter
4. We recommend you store the **"poNumber"** that you pass in the request and the **"orderID"** you receive in the response
5. Should you get a 5xx error from the PlaceOrderAPI, please call [GetOrderDetails](https://developers.xoxoday.com/v1.2/reference/get-order-details-api-1) and confirm if an order exists using the poNumber. If there's no order against the poNumber, you can go ahead and place another order

> Learn how to manage [webhooks](https://developers.xoxoday.com/v1.2/docs/webhooks-1) to receive order status updates for delayed product types.
