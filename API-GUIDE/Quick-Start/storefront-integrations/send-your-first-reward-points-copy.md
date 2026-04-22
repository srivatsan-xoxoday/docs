---
title: "Step by Step Guide for Storefront Integration"
slug: "send-your-first-reward-points-copy"
excerpt: "Send Your First Reward P"
hidden: false
createdAt: "Tue Aug 26 2025 13:46:11 GMT+0000 (Coordinated Universal Time)"
updatedAt: "Tue Dec 02 2025 10:17:39 GMT+0000 (Coordinated Universal Time)"
---
### Authentication

Create an API key in your sandbox (and production) dashboard.

### Set up Get Balance API

Xoxoday will call the client’s Point Balance API to fetch the end user’s available points.

1. Endpoint should accept POST JSON: 
```
{ "unique_id": "...", "auth_token": "..." }.
```
2. Validate auth_token and return JSON only. Expected response schema (sample):

```json
{  
  "status": "1",  
  "data": {  
    "unique_id": "DB123",  
    "points": "400"  
  }  
}
```

3. status: 1 = success, 0 = failure.
4. Notes: prefer numeric points but accept either; ensure HTTP 200 on success and JSON error body on failure.

### Set up Update Redemption API

The Update Redemption Transaction API allows Xoxoday to post redemption information to the client’s system whenever a user redeems points.

1. Endpoint accepts POST JSON with redemption details, e.g.:

```json
{  
  "unique_id":"TTEO32S99ERCL",  
  "auth_token":"<token>",  
  "total_points_redeemed": 348.5,  
  "order_id":"AB1890082790",  
  "order_date": 1693995688,  
  "orderData":[ ... ]  
}
```

2. Validate auth_token, persist order, update user points. Return JSON sample:

```json
{
  "status": "1",
  "message": "Successfully updated",
  "data": {
    "order_id": "12345"
  }
}
```

### Set up Get Profile API

The Get Profile API is used to verify account information and prevent fraud at the time of checkout. This API provides a second layer of account verification before the reward is sent, ensuring a seamless and secure customer experience.

1. Endpoint accepts POST JSON: 
```
{ "auth_token":"...", "unique_id":"..." }.
```
2. Return user profile as user_data with fields such as unique_id, email, first_name, last_name, primary_mobile_number, designation, department, group_company. Sample:

```json
{
  "status": 1,
  "message": "Successfully loaded user's data",
  "user_data": {
    "unique_id": "22816281",
    "email": "john.doe@example.com",
    "first_name": "John",
    "phone": "+1-1234567890"
  }
}
```

3. Use this call during checkout to verify identity and reduce fraud.

### Set up Refund API

The RefundAPI allows clients to automate the refund process for their users. It ensures that points are credited back seamlessly without manual intervention.

1. Endpoint accepts POST JSON: 
```
{ "auth_token":"...", "unique_id":"...", "transactionid":"...", "redemption_amount":"200" }.
```
2. Validate and credit points back to the user. Respond with JSON:

```json
{
  "status": "1",
  "message": "Successfully updated",
  "data": {
    "transaction_id": "AB1890082790",
    "points": "200"
  }
}
```

3. Support partial refunds and idempotency (use transactionid).

### Share the APIs & integration details with Xoxoday (for mapping/configuration)

Provide the following to the Xoxoday integration team so we can map attributes and configure your integration:

1. Endpoint paths for each API (balance, profile, update redemption, refund).

### Setup the SSO flow (call SSO Redirection API)

During your SSO flow, call Xoxoday SSO Redemption API with user_input and tpd (including the auth_token you want Xoxoday to use). Example minimal SSO body:

```json
{
  "user_input": "john.doe@example.com",
  "tpd": {
    "auth_token": "Your own key",
    "unique_id": "736517181",
    "email": {
      "default_value": "john.doe@example.com",
      "editable": true,
      "hidden": false,
      "support_alternate": true
    },
    "phone": {
      "default_value": "987654321",
      "phone_code": "+91",
      "editable": false,
      "hidden": false
    },
    "otp": "primary_email"
  }
}
```

<br />

Xoxoday responds with data.ssoToken. Redirect the user to:

1. Staging OAuth URL: https://stagingstores.xoxoday.com/chef/v1/oauth/redirect/stores/{ssoToken}
2. Production OAuth URL: https://stores.xoxoday.com/chef/v1/oauth/redirect/stores/{ssoToken}

**Note**: ssoToken is valid for 14 days by default.

### Test the full flow (end-to-end checks)

1. SSO redirect → new user creation or existing user fetch → receives ssoToken.
2. After redirect, Xoxoday calls Get Balance → validate points returned.
3. At checkout, Xoxoday calls Get Profile → ensure returned profile matches and verification passes.
4. On redemption, Xoxoday calls Update Redemption → validate order is created in your system and points deducted. Check idempotency by re-sending same order_id.
5. Simulate failures (inventory/fulfilment failure) → Xoxoday calls Refund API → validate refund and points credit.
6. Logging & monitoring: ensure you log incoming requests, validation errors, and responses; monitor for 4xx/5xx rates.
