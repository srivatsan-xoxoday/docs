---
title: "Place Order API"
slug: "place-order-api-2"
excerpt: "The PlaceOrderAPI enables the client to place an order for Merchandise available with Xoxoday"
hidden: false
createdAt: "Thu May 15 2025 07:32:15 GMT+0000 (Coordinated Universal Time)"
updatedAt: "Sat Nov 22 2025 22:00:48 GMT+0000 (Coordinated Universal Time)"
openapi: "API-PLAYGROUND/Rewards-API/merchandise/spec.yaml POST /placeOrder"
---
> A unique reference ID needs to be sent for every unique order in the "poNumber" parameter
>
> We strongly recommend storing the request and response of every "PlaceOrderAPI" call

## Request Parameter

| **Path**                 | **Type** | **Description**                                       |
| ------------------------ | -------- | ----------------------------------------------------- |
| data                     | object   | Root request wrapper.                                 |
| data.productId           | string   | Product ID of the merchandise item.                   |
| data.quantity            | number   | Quantity of the merchandise item.                     |
| data.denomination        | number   | Denomination/price of the product.                    |
| data.email               | string   | Customer email for notifications.                     |
| data.contact             | string   | Customer phone number.                                |
| data.tag                 | string   | Custom tag passed for tracking.                       |
| data.poNumber            | string   | Client-generated PO number (idempotency key).         |
| data.notifyReceiverEmail | number   | Whether the receiver gets an email (`1` = yes).       |
| data.notifyAdminEmail    | number   | Whether admin gets an email notification (`1` = yes). |
| data.shippingFirstName   | string   | Shipping first name.                                  |
| data.shippingLastName    | string   | Shipping last name.                                   |
| data.shippingContactNo   | string   | Shipping contact number.                              |
| data.shippingCompany     | string   | Company name for shipping.                            |
| data.shippingAddress1    | string   | Primary shipping address.                             |
| data.shippingAddress2    | string   | Secondary shipping address.                           |
| data.shippingCity        | string   | Shipping city.                                        |
| data.shippingCountry     | string   | Shipping country.                                     |
| data.shippingState       | string   | Shipping state/province/region.                       |
| data.shippingPostcode    | string   | Postal/ZIP code for the shipping address.             |

## Response Parameter

| **Path**                                             | **Type** | **Description**                                          |
| ---------------------------------------------------- | -------- | -------------------------------------------------------- |
| data                                                 | object   | Root response object.                                    |
| data.placeOrder                                      | object   | Container for order response.                            |
| data.placeOrder.status                               | number   | Request status (`1` = success).                          |
| data.placeOrder.data                                 | object   | Full order details.                                      |
| data.placeOrder.data.orderId                         | number   | Unique order ID.                                         |
| data.placeOrder.data.orderTotal                      | number   | Order total (rounded).                                   |
| data.placeOrder.data.rawOrderTotal                   | number   | Precise unrounded order amount.                          |
| data.placeOrder.data.orderDiscount                   | string   | Discount amount (blank if none).                         |
| data.placeOrder.data.rawOrderDiscount                | string   | Unrounded discount (blank if none).                      |
| data.placeOrder.data.discountPercent                 | string   | Discount percent applied.                                |
| data.placeOrder.data.currencyCode                    | string   | Currency code used for pricing.                          |
| data.placeOrder.data.currencyValue                   | number   | Currency conversion multiplier.                          |
| data.placeOrder.data.amountCharged                   | number   | Final amount charged.                                    |
| data.placeOrder.data.orderStatus                     | string   | Order lifecycle status (`complete`).                     |
| data.placeOrder.data.deliveryStatus                  | string   | Delivery status (`pending`).                             |
| data.placeOrder.data.tag                             | string   | Tag passed from request.                                 |
| data.placeOrder.data.quantity                        | number   | Quantity ordered.                                        |
| data.placeOrder.data.vouchers                        | array    | Always empty for merchandise (no instant code delivery). |
| data.placeOrder.data.voucherDetails                  | array    | Summary of merchandise items ordered.                    |
| data.placeOrder.data.voucherDetails\[].orderId       | number   | Order ID.                                                |
| data.placeOrder.data.voucherDetails\[].productId     | number   | Merchandise product ID.                                  |
| data.placeOrder.data.voucherDetails\[].productName   | string   | Product name.                                            |
| data.placeOrder.data.voucherDetails\[].currencyCode  | string   | Currency code of the merchandise.                        |
| data.placeOrder.data.voucherDetails\[].productStatus | string   | Status of merchandise fulfillment.                       |
| data.placeOrder.data.voucherDetails\[].denomination  | number   | Product denomination/price.                              |

## Implementation Notes

1. To avoid facing an error while placing an order, please pass the valid productID and denomination
2. The maximum order quantity allowed for the majority of the products is 10 unless mentioned otherwise in the **"orderQuantityLimit"** parameter in the GetVouchersAPI
3. Certain brands require a phone number to process the order. You can refer to the **"isPhoneNumberMandatory"** parameter in the GetVouchersAPI to identify the products with this mandate
4. Should you wish to notify the recipient via email, please pass "1" in the **"notifyReceiverEmail"** parameter
5. We recommend you store the **"poNumber"** that you pass in the request and the **"orderID"** you receive in the response
6. Should you get a 5xx error from the PlaceOrderAPI, please call [GetOrderDetails](https://developers.xoxoday.com/v1.2/reference/get-order-details-api-3) and confirm if an order exists using the poNumber. If there's no order against the poNumber, you can go ahead and place another order

> Learn how to manage [webhooks](https://developers.xoxoday.com/v1.2/docs/webhooks-1) to receive order status updates for delayed product types.
