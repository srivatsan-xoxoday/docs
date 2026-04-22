## How It Works

1. Access tokens expire after 15 days.
2. Refresh tokens can be used to generate new access tokens programmatically.
3. When a new access token is generated using a refresh token, you will also receive a new refresh token. The old refresh token becomes invalid and must be replaced in your system.

## Why It Matters

If your access token expires, your API calls will fail. Automating the refresh process ensures uninterrupted API connectivity without manual intervention.

## Steps to Generate a New Access Token

1. Use a previously obtained refresh token (from the initial OAuth setup).
2. Call the Refresh Token API to get:
   1. A new access token
   2. A new refresh token
   3. Expiry details for the access token in EPOCH format

Replace the old refresh token in your system with the new one returned in the response.

<ResponseField name="Token Invalidation Instances" type="string">
  <ResponseField name="Error Code" type="string">
    <ResponseField name="Super Admin resets their account's password" type="string">
      ```json
      {
        "success": 0,
        "error_message_id": "auth.token_error"
      }
      ```
    </ResponseField>
    <ResponseField name="Super Admin adds another Super Admin and the new Super Admin generates a new token" type="string">
      ```json
      {
        "error": "invalid_token",
        "error_description": "invalid/expired token"
      }
      ```
    </ResponseField>
    <ResponseField name="Unusual number of requests on Refresh Token API" type="string">
      ```json
      {
        "message": "auth.request_limit_exceeded"
      }
      ```
    </ResponseField>
  </ResponseField>
</ResponseField>

<br />

## Important Notes

1. Every time you use the refresh token, you will receive a new refresh token — always replace the old one.
2. If a 4xx error occurs, generate new tokens using the Refresh Token API.
3. Access tokens can be regenerated programmatically, but refresh tokens cannot — once expired, a new refresh token must be generated from the dashboard.
4. Xoxoday may invalidate your token for security reasons, such as:
   1. Super Admin password reset
   2. Addition of another Super Admin generating a new token
   3. Unusual number of refresh requests

## Best Practices

1. Refresh tokens every 7 days or before your access token expires.
2. Use a CRON job or scheduler to automatically refresh and store tokens.
3. Monitor expires_in in the response to know token lifetime in seconds.