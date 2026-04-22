---
title: "Refresh Token"
slug: "refresh-token"
excerpt: "Get the access token using the refresh token.  Get familiar with the API endpoint with request and response."
hidden: false
metadata: 
  title: "Refresh Token"
  description: "Get the access token using the refresh token.  Get familiar with this API endpoint by trying the request and response."
  image: []
  robots: "index"
createdAt: "Tue Apr 04 2023 10:47:13 GMT+0000 (Coordinated Universal Time)"
updatedAt: "Sat Nov 22 2025 20:54:51 GMT+0000 (Coordinated Universal Time)"
openapi: "API-PLAYGROUND/Rewards-API/authentication/spec.yaml POST /token/user"
---
## Request Schema

| **Parameter**     | **Type** | **Required** | **Description**                                                                            |
| ----------------- | -------- | ------------ | ------------------------------------------------------------------------------------------ |
| **grant_type**    | string   | Yes          | Must be `"refresh_token"` for this API.                                                    |
| **refresh_token** | string   | Yes          | The previously issued refresh token used to obtain a new access token.                     |
| **client_id**     | string   | Yes          | The client identifier provided by Xoxoday.                                                 |
| **client_secret** | string   | Yes          | The client secret associated with the client ID. Used to authenticate the refresh request. |

## Response Schema

| **Parameter**            | **Type** | **Description**                                                                              |
| ------------------------ | -------- | -------------------------------------------------------------------------------------------- |
| **access_token**         | string   | Newly issued access token to be used for authenticated API calls.                            |
| **token_type**           | string   | Token type. Always `"bearer"`.                                                               |
| **expires_in**           | number   | Lifetime of the access token in seconds.                                                     |
| **refresh_token**        | string   | Newly issued refresh token. Use this to generate new access tokens when current one expires. |
| **access_token_expiry**  | string   | Epoch timestamp (milliseconds) indicating expiry time of the access token.                   |
| **refresh_token_expiry** | string   | Epoch timestamp (milliseconds) indicating expiry of the refresh token.                       |

> 📘 Learn how to manage your access and refresh tokens [here](https://developers.xoxoday.com/v1.2/docs/refresh-token-access-token).
