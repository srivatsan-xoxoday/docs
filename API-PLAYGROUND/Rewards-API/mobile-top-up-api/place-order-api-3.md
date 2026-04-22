---
title: "Place Order API"
slug: "place-order-api-3"
excerpt: "With Place Order API, you can place orders for plans available in the Catalog."
hidden: false
createdAt: "Mon Jun 23 2025 09:20:40 GMT+0000 (Coordinated Universal Time)"
updatedAt: "Thu Jan 22 2026 05:43:09 GMT+0000 (Coordinated Universal Time)"
openapi: "API-PLAYGROUND/Rewards-API/mobile-top-up-api/spec.yaml POST /placeOrder"
---
> A unique reference ID needs to be sent for every unique order in the "poNumber" parameter
>
> We strongly recommend storing the request and response of every "PlaceOrderAPI" call

## Request Schema

| **Path**                        | **Type** | **Description**                                         |
| ------------------------------- | -------- | ------------------------------------------------------- |
| data                            | object   | Root request object.                                    |
| data.productId                  | number   | Product ID for the top-up plan.                         |
| data.quantity                   | number   | Quantity of the top-up purchase (always `1` typically). |
| data.denomination               | number   | Recharge/top-up amount.                                 |
| data.email                      | string   | Customer email for notifications.                       |
| data.tag                        | string   | Optional tracking tag.                                  |
| data.poNumber                   | string   | Client-provided PO number (idempotency key).            |
| data.notifyReceiverEmail        | number   | Whether user gets email notification (`1` = yes).       |
| data.performOperatorValidation  | boolean  | Performs operator validation.                           |
| data.notifyAdminEmail           | number   | Whether admin receives notification (`1` = yes).        |
| data.userMeta                   | object   | Mobile top-up specific parameters.                      |
| data.topupData.topupPhoneCode   | string   | Country code prefix (e.g., `+91`).                      |
| data.topupData.topupPhoneNumber | string   | Mobile number to be recharged.                          |

## Response Schema

| **Path**                                             | **Type** | **Description**                        |
| ---------------------------------------------------- | -------- | -------------------------------------- |
| data                                                 | object   | Root response object.                  |
| data.placeOrder                                      | object   | Place order result.                    |
| data.placeOrder.status                               | number   | API execution status (`1` = success).  |
| data.placeOrder.data                                 | object   | Complete order details.                |
| data.placeOrder.data.orderId                         | number   | Unique order ID.                       |
| data.placeOrder.data.orderTotal                      | number   | Order total (rounded).                 |
| data.placeOrder.data.rawOrderTotal                   | number   | Exact unrounded order amount.          |
| data.placeOrder.data.orderDiscount                   | string   | Discount amount applied.               |
| data.placeOrder.data.rawOrderDiscount                | string   | Precise unrounded discount.            |
| data.placeOrder.data.discountPercent                 | string   | Discount percent.                      |
| data.placeOrder.data.currencyCode                    | string   | Currency code.                         |
| data.placeOrder.data.currencyValue                   | number   | Currency conversion multiplier.        |
| data.placeOrder.data.amountCharged                   | number   | Final charged amount.                  |
| data.placeOrder.data.orderStatus                     | string   | Order lifecycle status.                |
| data.placeOrder.data.deliveryStatus                  | string   | Delivery status (`pending`, etc.).     |
| data.placeOrder.data.tag                             | string   | Tag from request.                      |
| data.placeOrder.data.quantity                        | number   | Quantity ordered.                      |
| data.placeOrder.data.vouchers                        | array    | Always empty for top-up.               |
| data.placeOrder.data.voucherDetails                  | array    | Summary of top-up item(s).             |
| data.placeOrder.data.voucherDetails\[].orderId       | number   | Order ID.                              |
| data.placeOrder.data.voucherDetails\[].productId     | number   | Product ID.                            |
| data.placeOrder.data.voucherDetails\[].productName   | string   | Name of the telecom/data top-up.       |
| data.placeOrder.data.voucherDetails\[].currencyCode  | string   | Currency code for the product.         |
| data.placeOrder.data.voucherDetails\[].productStatus | string   | Status (`pending`).                    |
| data.placeOrder.data.voucherDetails\[].denomination  | number   | Recharge amount.                       |
| data.placeOrder.data.voucherDetails\[].vendorLogo    | string   | Logo of telecom vendor (may be empty). |
| data.placeOrder.data.orderMeta                       | object   | Metadata passed in request.            |
| data.placeOrder.data.orderMeta.email                 | string   | Email submitted during request.        |

## Implementation Notes

1. To avoid facing an error while placing an order, please pass the valid productID and denomination
2. The maximum order quantity allowed for the products is 1 as mentioned  in the **"orderQuantityLimit"** parameter in the GetVouchersAPI
3. Should you wish to notify the recipient via email, please pass "1" in the **"notifyReceiverEmail"** parameter
4. We recommend you store the **"poNumber"** that you pass in the request and the **"orderID"** you receive in the response
5. A new boolean parameter, **performOperatorValidation**, has been introduced. When set to **0,** no operator validation is performed and the order is attempted directly using the operator provided in the request. When set to 1, the system validates the requested operator against the operator identified from the vendor; if both match, the order proceeds successfully, and if they do not match, the order is rejected with an operator validation error.
6. Should you get a 5xx error from the PlaceOrderAPI, please call [GetOrderDetails](https://developers.xoxoday.com/v1.2/reference/get-order-details-api-4) and confirm if an order exists using the poNumber. If there's no order against the poNumber, you can go ahead and place another order

> Learn how to manage [webhooks](https://developers.xoxoday.com/v1.2/docs/webhooks-1) to receive order status updates for delayed product types.
