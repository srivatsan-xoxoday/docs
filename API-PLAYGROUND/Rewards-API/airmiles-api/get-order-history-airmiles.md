---
title: "Get Order History"
slug: "get-order-history-airmiles"
excerpt: "Fetch Order History API, allows you to fetch all the orders placed for Airmiles category for a specific timeline"
hidden: false
createdAt: "Wed Nov 12 2025 12:48:20 GMT+0000 (Coordinated Universal Time)"
updatedAt: "Wed Feb 04 2026 19:40:31 GMT+0000 (Coordinated Universal Time)"
openapi: "API-PLAYGROUND/Rewards-API/airmiles-api/spec.yaml POST /getOrderHistory"
---
## Request Schema

| Parameter | Type   | Description                                                                 |
| :-------- | :----- | :-------------------------------------------------------------------------- |
| startDate | String | Start date for filtering records.                                           |
| endDate   | String | End date for filtering records.                                             |
| limit     | Int    | Number of records to return per page (pagination).                          |
| page      | Int    | Page number to fetch when paginating results.                               |
| tag       | String | Custom tag to filter or group records by campaign, user, or other metadata. |

## Response Schema

| **Path**                                                      | **Type**    | **Description**                                                      |
| ------------------------------------------------------------- | ----------- | -------------------------------------------------------------------- |
| data                                                          | object      | Root response object.                                                |
| data.getOrderHistory                                          | object      | Container for order history.                                         |
| data.getOrderHistory.status                                   | number      | API execution status (`1` = success).                                |
| data.getOrderHistory.data                                     | array       | List of historical orders (generic across all categories).           |
| data.getOrderHistory.data\[].orderId                          | number      | Unique order ID.                                                     |
| data.getOrderHistory.data\[].orderDate                        | string      | Order creation timestamp.                                            |
| data.getOrderHistory.data\[].email                            | string      | Email used for the order.                                            |
| data.getOrderHistory.data\[].deliveryStatus                   | string      | Delivery status (`pending`, `delivered`).                            |
| data.getOrderHistory.data\[].poNumber                         | string      | PO number passed during checkout.                                    |
| data.getOrderHistory.data\[].tag                              | string/null | Custom tag (generic).                                                |
| data.getOrderHistory.data\[].orderTotal                       | number      | Rounded order amount.                                                |
| data.getOrderHistory.data\[].rawOrderTotal                    | number/null | Unrounded order amount (may be NULL for older orders).               |
| data.getOrderHistory.data\[].orderDiscount                    | number      | Discount applied.                                                    |
| data.getOrderHistory.data\[].rawOrderDiscount                 | number/null | Exact unrounded discount (may be NULL).                              |
| data.getOrderHistory.data\[].discountPercent                  | number      | Discount percentage.                                                 |
| data.getOrderHistory.data\[].amountCharged                    | number      | Final charged amount.                                                |
| data.getOrderHistory.data\[].currencyValue                    | number      | FX conversion multiplier.                                            |
| data.getOrderHistory.data\[].currencyCode                     | string      | Currency code of the order.                                          |
| data.getOrderHistory.data\[].products                         | array       | List of ordered products (generic across all categories).            |
| data.getOrderHistory.data\[].products\[].productId            | number      | Product ID (generic across voucher/lounge/merchandise/top-up/perks). |
| data.getOrderHistory.data\[].products\[].productName          | string      | Product name.                                                        |
| data.getOrderHistory.data\[].products\[].receiverMobileNumber | string      | Receiver mobile number                                               |
| data.getOrderHistory.data\[].products\[].receiverEmail        | string      | Receiver email (generic).                                            |
| data.getOrderHistory.data\[].products\[].price                | number      | Price/denomination/value.                                            |
| data.getOrderHistory.data\[].products\[].quantity             | number      | Ordered quantity.                                                    |
| data.getOrderHistory.data\[].products\[].orderProductStatus   | string      | Status of the individual product item (generic).                     |
| data.getOrderHistory.data\[].products\[].currency             | string      | Currency code for the product.                                       |
| data.getOrderHistory.data\[].products\[].trackingId           | string/null | Shipment tracking ID **(merchandise only)**.                         |
| data.getOrderHistory.data\[].products\[].trackingLink         | string/null | Shipment tracking URL **(merchandise only)**.                        |
| data.getOrderHistory.data\[].voucherDetails                   | array       | Summary of voucher/lounge/product info (all categories).             |
| data.getOrderHistory.data\[].voucherDetails\[].orderId        | number      | Order ID.                                                            |
| data.getOrderHistory.data\[].voucherDetails\[].productId      | number      | Product ID.                                                          |
| data.getOrderHistory.data\[].voucherDetails\[].productName    | string      | Product name.                                                        |
| data.getOrderHistory.data\[].voucherDetails\[].currencyCode   | string      | Currency code.                                                       |
| data.getOrderHistory.data\[].voucherDetails\[].productStatus  | string      | Cancelled Or Delivered                                               |
| data.getOrderHistory.data\[].voucherDetails\[].denomination   | number      | Product denomination/value.                                          |

## Implementation Notes

1. To fetch all the orders within a specified timeframe, pass a higher value in the **"limit"** parameter and pass the value as "1" in the **"page"** parameter

> **How Customers use this getOrderHistory API ?**
>
> Customer who have their own internal reporting systems or those personas who want to know the historic data of the transactions for internal auditing purpose, use this endpoint to fetch the order history for a specified time.
