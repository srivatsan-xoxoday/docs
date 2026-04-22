---
title: "Concepts"
slug: "concepts-1"
excerpt: ""
hidden: false
createdAt: "Fri Aug 08 2025 10:42:00 GMT+0000 (Coordinated Universal Time)"
updatedAt: "Wed Jan 28 2026 08:02:24 GMT+0000 (Coordinated Universal Time)"
---
This article will help you understand the key concepts you need to start working with the Xoxoday Rewards API quickly and confidently.

The following sections cover the essential elements of the API, so you can design, test, and deploy your integration without surprises.

## Staging Environment

The Xoxoday staging environment is a free, fully-featured space for application development and testing. It supports all endpoints and functionality of the Rewards API, but with demo balances and a limited product catalog. 

- Develop and test your application against staging first.
- Switch to production only when you’re ready to go live.

📘 Products & Denominations  
The staging environment supports a limited set of products and denominations. Click [here](https://stagingstores.xoxoday.com/marketplace/rewards-api-catalogue) for the full list available in staging.

## Catalog

The Xoxoday Rewards API provides access to a large collection of digital vouchers across multiple categories.

### Refreshing the Catalog

To ensure you always have the latest product details, denominations, images, and terms & conditions, we recommend refreshing the catalog four times per day at:

- 12:00 AM
- 06:00 AM
- 12:00 PM
- 06:00 PM

All timings are in GMT+5:30 (India Time Zone).

## Order Fulifment

Our product catalog includes two types of products based on delivery behavior:

1. **Real-Time Products**
   1. Definition: Orders are processed and fulfilled instantly.
   2. Response Time: You’ll receive a success or failure response within 120 seconds.
   3. Use Case: Perfect for instant gratification and time-sensitive rewards.
2. **Delayed Gift Products**
   1. Definition: Orders are placed into a pending state and fulfilled later.
   2. Fulfilment Time: Delivered within the estimated time provided in the API response (typically 3–10 working days).
   3. Use Case: Works well when a short delivery delay is acceptable.

## PO Number (Purchase Order Number)

A PO Number (Purchase Order Number) is a unique reference ID that you, as a client, can generate and pass while placing an order through the Xoxoday API.

### Purpose:

1. Acts as an additional identifier for your orders, beyond the system-generated orderId.
2. Prevents duplicate orders — if the same PO number is used again, the system will reject the request.
3. Helps in reconciling orders easily during audits and reporting, since you can match transactions in your internal systems with the orders placed on Xoxoday.

### Example Use Case:

If your system sends the same order request twice due to a retry or timeout, the PO number ensures that only one order is created.

### Recommendation:

Always pass a unique PO number from your system when placing orders.

> ⚠️ Note: Use the deliveryType field in the GetVouchers API response to determine if a product is realtime or delayed.

## Recommended Practices

Follow these guidelines to ensure smooth API consumption and integration:

1. **Catalog Refresh**  
   Sync your catalog four times daily (12:00 AM, 06:00 AM, 12:00 PM, 06:00 PM) to always have the latest products and data.

2. **Use of PO Number**  
   Implement the PO number field to avoid placing duplicate orders.

3. **API Timeout Handling**  
   Allow up to 120 seconds for API responses, especially for real-time gift cards, due to possible vendor system delays.

4. **Error Code Handling**  
   Leverage the wide range of error codes provided in API responses to improve error handling and provide clear user feedback.

## Authentication Overview

All requests to the Reward APIs and Reward Links APIs must be authenticated.

> Note: Xoxoday uses the standard OAuth 2.0 protocol and a RESTful Rewards API to enable seamless voucher integrations.

The overall authentication process remains the same across Reward APIs, Reward Links APIs, Storefront Integration APIs, and Reward Points APIs. The only difference lies in how tokens are generated and the validity period of these tokens.

1. Reward APIs and Reward Links APIs → Same process for token generation and validity.
2. Storefront Integration APIs and Reward Points APIs → Follow a different, but common, process for token generation and validity.

For complete details, refer to the dedicated authentication documentation for each API type:

1. [Reward APIs & Reward Links APIs Authentication](https://developers.xoxoday.com/v1.2/docs/authentication-2)
2. [Storefront Integration APIs & Reward Points APIs Authentication](https://developers.xoxoday.com/v1.2/docs/authentication-copy)
