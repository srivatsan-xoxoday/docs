---
title: "Get Order Details API"
slug: "get-order-details-api-4"
excerpt: "With Fetch Order Details API, you can fetch the order details of a specific order by passing the order ID or Po Number."
hidden: false
createdAt: "Mon Jun 23 2025 11:17:19 GMT+0000 (Coordinated Universal Time)"
updatedAt: "Sat Nov 22 2025 22:24:06 GMT+0000 (Coordinated Universal Time)"
openapi: "API-PLAYGROUND/Rewards-API/mobile-top-up-api/spec.yaml POST /getOrderDetails"
---
## Request Schema

| Parameter          | Type      | Description                                                    |
| :----------------- | :-------- | :------------------------------------------------------------- |
| poNumber           | String    | Purchase Order number to avoid duplicate orders.               |
| orderId            | Float     | Unique ID of the order (used for referencing existing orders). |
| sendMailToReceiver | Int (0/1) | Flag to notify the recipient via email (1 = Yes, 0 = No).      |

## Response Schema

| **Path**                                                      | **Type**    | **Description**                                                             |
| ------------------------------------------------------------- | ----------- | --------------------------------------------------------------------------- |
| data                                                          | object      | Root response object.                                                       |
| data.getOrderDetails                                          | object      | Container for order details.                                                |
| data.getOrderDetails.status                                   | number      | API execution status (`1` = success).                                       |
| data.getOrderDetails.data                                     | object      | Order details payload.                                                      |
| data.getOrderDetails.data.orderId                             | number      | Unique order ID                                                             |
| data.getOrderDetails.data.orderTotal                          | number      | Rounded total amount                                                        |
| data.getOrderDetails.data.rawOrderTotal                       | number      | Exact unrounded amount                                                      |
| data.getOrderDetails.data.orderDiscount                       | string      | Discount applied; may be blank (generic).                                   |
| data.getOrderDetails.data.rawOrderDiscount                    | string      | Exact unrounded discount                                                    |
| data.getOrderDetails.data.discountPercent                     | string      | Discount percent                                                            |
| data.getOrderDetails.data.currencyCode                        | string      | Currency code                                                               |
| data.getOrderDetails.data.currencyValue                       | number      | FX multiplier                                                               |
| data.getOrderDetails.data.amountCharged                       | number      | Final charged amount                                                        |
| data.getOrderDetails.data.orderStatus                         | string      | Order completion status                                                     |
| data.getOrderDetails.data.deliveryStatus                      | string      | Delivery status                                                             |
| data.getOrderDetails.data.tag                                 | string      | Custom tag from request                                                     |
| data.getOrderDetails.data.orderDate                           | string      | Order creation timestamp                                                    |
| data.getOrderDetails.data.deliveryDate                        | string      | Delivery timestamp; blank if pending                                        |
| data.getOrderDetails.data.quantity                            | number      | Ordered quantity                                                            |
| data.getOrderDetails.data.shippingDetails                     | object      | Shipping details **(only for merchandise; empty for other categories)**.    |
| data.getOrderDetails.data.shippingDetails.shippingFirstName   | string      | First name **(merchandise only)**.                                          |
| data.getOrderDetails.data.shippingDetails.shippingLastName    | string      | Last name **(merchandise only)**.                                           |
| data.getOrderDetails.data.shippingDetails.shippingContactNo   | string      | Shipping contact **(merchandise only)**.                                    |
| data.getOrderDetails.data.shippingDetails.shippingCompany     | string      | Company name **(merchandise only)**.                                        |
| data.getOrderDetails.data.shippingDetails.shippingAddress1    | string      | Address line 1 **(merchandise only)**.                                      |
| data.getOrderDetails.data.shippingDetails.shippingAddress2    | string      | Address line 2 **(merchandise only)**.                                      |
| data.getOrderDetails.data.shippingDetails.shippingCity        | string      | Shipping city **(merchandise only)**.                                       |
| data.getOrderDetails.data.shippingDetails.shippingState       | string      | Shipping state **(merchandise only)**.                                      |
| data.getOrderDetails.data.shippingDetails.shippingCountry     | string      | Shipping country **(merchandise only)**.                                    |
| data.getOrderDetails.data.shippingDetails.shippingPostcode    | string      | Postal/ZIP code **(merchandise only)**.                                     |
| data.getOrderDetails.data.vouchers                            | array       | Delivered voucher codes.                                                    |
| data.getOrderDetails.data.vouchers\[].productId               | number      | Product ID                                                                  |
| data.getOrderDetails.data.vouchers\[].voucherCode             | string      | Voucher code                                                                |
| data.getOrderDetails.data.vouchers\[].pin                     | string      | PIN                                                                         |
| data.getOrderDetails.data.vouchers\[].validity                | string      | Expiry date                                                                 |
| data.getOrderDetails.data.vouchers\[].amount                  | number      | Voucher amount                                                              |
| data.getOrderDetails.data.vouchers\[].currency                | string      | Voucher currency                                                            |
| data.getOrderDetails.data.voucherDetails                      | array       | Summary of items in order (generic across all categories).                  |
| data.getOrderDetails.data.voucherDetails\[].orderId           | number      | Order ID (generic).                                                         |
| data.getOrderDetails.data.voucherDetails\[].productId         | number      | Product ID (generic).                                                       |
| data.getOrderDetails.data.voucherDetails\[].productName       | string      | Product name (generic).                                                     |
| data.getOrderDetails.data.voucherDetails\[].currencyCode      | string      | Product currency (generic).                                                 |
| data.getOrderDetails.data.voucherDetails\[].productStatus     | string      | Delivery status (generic).                                                  |
| data.getOrderDetails.data.voucherDetails\[].denomination      | number      | Voucher value / lounge price / merchandise price / top-up amount (generic). |
| data.getOrderDetails.data.voucherDetails\[].cancelledQuantity | number      | Cancelled quantity                                                          |
| data.getOrderDetails.data.voucherDetails\[].trackingId        | string/null | Shipment tracking ID **(merchandise only)**.                                |
| data.getOrderDetails.data.voucherDetails\[].trackingLink      | string/null | Tracking URL **(merchandise only)**.                                        |
| data.getOrderDetails.data.orderMeta                           | object      | Additional metadata captured during place order (category-specific).        |

## Implementation Notes

1. We do not recommend calling GetOrderDetails API to poll the order status for delayed delivery orders. Instead, implement [Webhooks](https://developers.xoxoday.com/v1.2/docs/webhooks-1) to be notified when an order status is changed
2. You can fetch order details by either using poNumber OR orderId
3. When you pass poNumber as a String, accepted values for orderId:
   1. Null value. Example: `orderId: null`
   2. 0 as an integer. Example: `orderId: 0`
   3. 0 as a string. Example: `orderId: "0"`
4. When you only pass orderId, valid cases: 
   1. Case 1:
      - `poNumber: ""`
      - `orderId: "26663453"`
   2. Case 2:
      - `poNumber: ""`
      - `orderId: 26663453`
   3. Case 3:
      - `poNumber: null`
      - `orderId: 26663453`
   4. Case 4:
      - `poNumber: null`
      - `orderId: "26663453"`

This ensures that the Get Order Details API works correctly in different situations.
