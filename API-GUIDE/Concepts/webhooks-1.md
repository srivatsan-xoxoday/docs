---
title: "Webhooks"
slug: "webhooks-1"
excerpt: "The Rewards API supports webhooks to receive real-time updates on order statuses. This allows your system to automatically track order delivery without the need for repeated API polling."
hidden: false
createdAt: "Sun Aug 10 2025 14:54:12 GMT+0000 (Coordinated Universal Time)"
updatedAt: "Tue Aug 19 2025 11:00:28 GMT+0000 (Coordinated Universal Time)"
---
> Note: Webhooks are only functional for Plum Pro APIs. They are not supported with Marketplace Integration, Reward Link API and Reward Points API.

You can use the webhook testing feature to:

1. Validate payloads received from Plum Pro.
2. Verify that your webhook integration is set up correctly.

Test events are triggered when a transaction occurs in the staging environment.  
There are two ways to test webhooks:

1. Using free interceptor tools (e.g., requestbin.com)
2. On your staging environment

## Using Free Interceptor Tools

Many free webhook testing tools are available online. For example: requestbin.com.

Steps to Test

1. Step 1: Open requestbin.com in your web browser.
2. Step 2: Click "Create a RequestBin" to start.
3. Step 3: Sign up by entering your details or log in via SSO.
4. Step 4: Copy the unique endpoint URL generated for you.
5. Step 5: In the Xoxoday Dashboard, go to the Settings>API and paste the endpoint into the Callback URL field. Click "Save Webhook".

   ![](https://files.readme.io/495ac1b735261a569dacd57417fc2bbe453d9521852ef352d2e8a995fe48ff50-image.png)
6. Step 6: Once you enable the appropriate webhook event, you will receive the corresponding webhook payload on your requestbin.com.
