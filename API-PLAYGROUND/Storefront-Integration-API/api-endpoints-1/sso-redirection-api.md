---
title: "SSO Redirection API"
slug: "sso-redirection-api"
excerpt: "The Single Sign-On (SSO) API allows seamless authentication of users into Xoxoday's StoreFront. It ensures that users can log in with their existing credentials from the your system."
hidden: false
createdAt: "Fri Apr 07 2023 07:44:17 GMT+0000 (Coordinated Universal Time)"
updatedAt: "Fri Mar 13 2026 08:19:31 GMT+0000 (Coordinated Universal Time)"
openapi: "storefront-spec.yaml POST /sso/stores/company"
---
## Key Pointers

1. The SSO API is based on SAML 2.0 standards.
2. If the user account does not exist in Xoxoday, one will be created automatically.
3. The API returns an ssoToken which is used for redirecting the user securely into the StoreFront.

## Implementation Details

### Headers

1. `Content-Type: application/json`
2. `Authorization: Bearer <access_token>`

**Note**: [Learn how to generate access token here.](https://developers.xoxoday.com/v1.2/docs/create-your-api-key-copy-2)

### Redirection URL format

```
{OAUTH_URL}/chef/v1/oauth/redirect/stores/{ssoToken} 
```

{OAUTH_URL} for: 

- Staging: https://stagingstores.xoxoday.com
- Production: https://stores.xoxoday.com

> Note: Replace the {ssoToken} with the SSO token received in the response of this API.

### Editable Fields at Checkout

1. Email and phone values can be marked as editable or non-editable at checkout.
2. Fields can also be hidden if you don’t want them shown to the user.

### OTP Verification

You can configure OTP validation for checkout on primary email, primary phone, alternate email, or disable it.

## SSO Redirection API Request Schema

| Parameter                     | Type    | Description                                                                                                                |
| ----------------------------- | ------- | -------------------------------------------------------------------------------------------------------------------------- |
| `user_input`                  | String  | End user’s email address. Used to create or fetch the account in Xoxoday.                                                  |
| `tpd`                         | Object  | Third-party data object containing user identity, authorization details and any custom parameter for each user.            |
| `tpd.auth_token`              | String  | Token provided by the client. Xoxoday will use this for subsequent API calls (balance, transaction, refund, verification). |
| `tpd.unique_id`               | String  | Unique identifier for the user                                                                                             |
| `tpd.email`                   | Object  | Email configuration object for the user.                                                                                   |
| `tpd.email.default_value`     | String  | Actual email ID of the user. Can be updated without affecting account history.                                             |
| `tpd.email.editable`          | Boolean | If `false`, the user cannot edit the email at checkout.                                                                    |
| `tpd.email.hidden`            | Boolean | If `true`, the email field will be hidden at checkout.                                                                     |
| `tpd.email.support_alternate` | Boolean | If `false`, no alternate email option will be shown.                                                                       |
| `tpd.phone`                   | Object  | Phone configuration object for the user.                                                                                   |
| `tpd.phone.default_value`     | String  | Phone number of the user.                                                                                                  |
| `tpd.phone.phone_code`        | String  | Country code of the phone number (e.g., `+91`).                                                                            |
| `tpd.phone.editable`          | Boolean | If `false`, the user cannot edit the phone number at checkout.                                                             |
| `tpd.phone.hidden`            | Boolean | If `true`, the phone field will be hidden at checkout.                                                                     |
| `tpd.otp`                     | String  | Mode of OTP validation. Possible values: `primary_email`, `primary_phone`, `alternate_email`, `none`.                      |

## Response Schema

| Parameter       | Type   | Description                                                                                                                            |
| --------------- | ------ | -------------------------------------------------------------------------------------------------------------------------------------- |
| `data.ssoToken` | String | Unique token generated upon successful validation. Used to redirect the user into Xoxoday StoreFront. Default validity is **14 days**. |
