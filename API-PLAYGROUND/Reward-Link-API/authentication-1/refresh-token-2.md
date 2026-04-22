---
title: "Refresh Token"
slug: "refresh-token-2"
excerpt: "Get the access token using the refresh token.  Get familiar with the API endpoint with request and response."
hidden: false
createdAt: "Mon Aug 25 2025 09:11:06 GMT+0000 (Coordinated Universal Time)"
updatedAt: "Mon Nov 24 2025 06:06:20 GMT+0000 (Coordinated Universal Time)"
openapi: "reward-link-spec.yaml POST /token/user"
---
> 📘 Learn how to manage your access and refresh tokens [here](https://developers.xoxoday.com/v1.2/docs/refresh-token-access-token).

## Request Schema

| **Property**  | **Type** | **Description**                                                      |
| ------------- | -------- | -------------------------------------------------------------------- |
| grant_type    | string   | Must be `"refresh_token"` to indicate token regeneration.            |
| refresh_token | string   | The existing refresh token used to generate a new access token.      |
| client_id     | string   | Client ID provided to you for authentication.                        |
| client_secret | string   | Client secret used to authenticate and validate the refresh request. |

## Response Schema

| **Property**  | **Type** | **Description**                              |
| ------------- | -------- | -------------------------------------------- |
| access_token  | string   | Newly generated access token.                |
| token_type    | string   | Type of token issued (`bearer`).             |
| expires_in    | number   | Access token validity duration (in seconds). |
| refresh_token | string   | New refresh token issued to the user.        |
