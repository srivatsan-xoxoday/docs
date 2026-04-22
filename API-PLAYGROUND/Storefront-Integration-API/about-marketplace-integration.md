---
title: "About Storefront Integration"
slug: "about-marketplace-integration"
excerpt: "This article briefly introduces Xoxoday's Storefront Integration"
hidden: false
createdAt: "Tue Apr 11 2023 12:31:36 GMT+0000 (Coordinated Universal Time)"
updatedAt: "Fri Sep 12 2025 14:08:36 GMT+0000 (Coordinated Universal Time)"
---
# Storefront Integration

With Xoxoday's Strorefront Integration, you can simply allow your users to be re-directed into Xoxoday's storefront/ marketplace.  Here you can simply provide SSO (Single Sign On) or SAML based authentication for your users to seamlessly login into Xoxoday's hosted Storefront.  

Below are the advantages the _**Storefront integration**_ has to offer that you may want to consider:

1. Use your platforms's native points engine to distribute points, while simply re-directing users onto Xoxoday's hosted Storefront to '_burn_' their accrued points.
2. A simple SSO or SAML based authentication to provide your users with a seamless access to storefornt.

Once users land in the storefront, our system will consume your end-points to `GET` points accrued in your system, and as well as `POST` back the points spent (by users) on their reward catalog.

# APIs Provided by Xoxoday

These APIs are built and exposed by Xoxoday for the client to use:

1. SSO Redirection API
   1. Enables end users to be redirected and authenticated via SAML 2.0.
   2. Issues an SSO Token upon successful authentication.
   3. Handles account creation if the user doesn’t exist in Xoxoday.

# APIs Required from Clients

Xoxoday will consume the following APIs from the client’s system in order to perform transactions and validate users:

## Get Balance API

This API is used to fetch a user’s accrued points that are available for redemption.

## Update Redemption API

This API is used to update the points spent by the user when placing an order on Xoxoday’s Storefront.  
It ensures that your system reflects the deduction in the user’s points balance.

Note: Xoxoday’s request will include:

1. Total points redeemed
2. Order ID
3. Array of objects containing order details

## Get Profile API

This API is used to validate user details (including points balance and user identity) during checkout, adding an additional layer of security.

> 📘 If the user’s points balance is included in the Get Profile API response, Xoxoday can use this endpoint directly instead of the Get Balance API.

## Refund API

This API is used to credit back the user’s points in cases where Xoxoday is unable to fulfill an order.  
Refunds are always issued against the original Xoxoday Order ID, and the refund amount cannot exceed the order value.

## All requests from Xoxoday are sent from the following IP addresses:

### Staging

1. 50.112.248.135
2. 54.184.56.156
3. 52.24.158.163
4. 34.217.113.26
5. 54.185.176.191

### Production

1. 52.76.120.90
2. 52.74.39.101
3. 52.221.42.47
4. 46.137.196.217

## All requests from Xoxoday are sent from the following domain(s):

Staging

1. https://canvas.xoxoday.com
2. https://canvas.plum.gift

Production

1. https://stores.xoxoday.com
2. https://accounts.xoxoday.com
3. https://app.xoxoday.com
4. https://plum.gift
