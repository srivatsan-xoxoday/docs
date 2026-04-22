---
title: "Storefront Integrations"
slug: "storefront-integrations"
excerpt: ""
hidden: false
createdAt: "Tue Aug 26 2025 14:16:07 GMT+0000 (Coordinated Universal Time)"
updatedAt: "Tue Jan 20 2026 13:15:11 GMT+0000 (Coordinated Universal Time)"
---
With Xoxoday's Strorefront Integration, you can simply allow your users to be re-directed into Xoxoday's storefront/ marketplace.  Here you can simply provide SSO (Single Sign On) or SAML based authentication for your users to seamlessly login into Xoxoday's hosted Storefront.  

Below are the advantages the _**Storefront integration**_ has to offer that you may want to consider:

1. Use your platforms's native points engine to distribute points, while simply re-directing users onto Xoxoday's hosted Storefront to '_burn_' their accrued points.
2. A simple SSO or SAML based authentication to provide your users with a seamless access to storefornt.

Once users land in the storefront, our system will consume your end-points to `GET` points accrued in your system, and as well as `POST` back the points spent (by users) on their reward catalog.

## APIs Provided by Xoxoday

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

***

We’ll create both a sandbox account and a live product account for you. Once access is granted, you can:

1. Log in to your Sandbox dashboard
2. Create your API key
3. Start exploring Storefront Integration.

## Standard Workflow for Storefront Integration.

![](https://files.readme.io/f5f3f223ff0595aaf897937eae11828582e585b522ce75a53f87a4811fc68372-Screenshot_2026-01-20_at_6.43.55PM.png)
