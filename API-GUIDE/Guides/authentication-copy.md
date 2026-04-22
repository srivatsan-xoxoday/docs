---
title: "Authentication - Storefront Integration APIs & Reward Points APIs"
slug: "authentication-copy"
excerpt: "Everything you need to know to securely connect with Storefront Integration APIs and Reward Points API."
hidden: false
createdAt: "Mon Aug 25 2025 06:31:31 GMT+0000 (Coordinated Universal Time)"
updatedAt: "Fri Oct 24 2025 07:34:06 GMT+0000 (Coordinated Universal Time)"
---
All requests to the Storefront Integration APIs and Reward Points APIs must be authenticated. This section explains how to create and manage tokens to ensure secure communication.

> Note: Xoxoday uses the standard OAuth 2.0 protocol and a RESTful Rewards API to let you integrate vouchers seamlessly into your environment.

### Authentication URLs

When you’re starting out, you can use a Sandbox account in our staging environment. Once you’re ready to go live, simply switch to the Production environment.

1. Sandbox Auth URL  
   https://stagingstores.xoxoday.com/chef
2. Production Auth URL  
   https://accounts.xoxoday.com/chef

### Client ID, Secret ID, and Token Creation

Xoxoday uses Bearer Authentication. Every API request must include your Access Token in the HTTP header.

You’ll first need to generate your Client ID and Secret ID from the admin portal. Once you have these, you can use them to create an Access Token.

Quick Steps:

1. Log in to your Admin Portal.
2. Navigate to API Credentials.
3. Copy your Client ID and Secret ID.
4. Generate your Access Token.

Copy your token immediately — it will not be shown again.

### Generating Tokens

For detailed, step-by-step instructions on generating your Client ID, Secret ID, and Access Token, visit [Create your API Key.](https://developers.xoxoday.com/v1.2/docs/create-your-api-key-copy)

### IP Whitelisting

For security, only whitelisted IPs can access the APIs.  
Please share your staging and production IP addresses with your Implementation Manager to get them whitelisted.
