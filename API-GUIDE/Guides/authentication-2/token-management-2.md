---
title: "Token Management"
slug: "token-management-2"
excerpt: "This document provides detailed information about the management and lifecycle of access and refresh tokens in the system. It outlines the behavior of tokens, the processes for token regeneration, and recommendations for optimal token usage."
hidden: false
createdAt: "Fri Aug 08 2025 12:07:56 GMT+0000 (Coordinated Universal Time)"
updatedAt: "Tue Aug 26 2025 14:26:49 GMT+0000 (Coordinated Universal Time)"
---
## Token Behavior and Regeneration Process

### Token Expiry

1. **Refresh Token Expiry**: Refresh tokens expire 30 days after generation.
2. **Access Token Expiry**: Access tokens expire 15 days after generation.

### Token Invalidation and Generation

When a refresh process occurs, the old access and refresh tokens are not immediately invalidated.

### Regeneration Process

Access Token Validity:

The old access token remains valid until its original expiry date.  
For example, if an access token was set to expire on November 16, it will retain this expiry date even after a new token is generated.

### Refresh Token Validity Window:

After initiating a refresh, the old refresh token remains valid for an additional 6 hours.  
This window allows multiple servers or clusters enough time to refresh their tokens.  
After this 6-hour window, the old refresh token will no longer be valid.

### Maximum Concurrent Tokens:

There is a cap of 10 active access and refresh token pairs per client.  
If more than 10 concurrent refreshes occur, the oldest token pair (access and refresh) will be invalidated to maintain the cap.

### Single Active Token Pair:

A client can only have one active token pair at any moment.  
This means managing token generation and refresh carefully to ensure that no unexpected invalidation occurs.

## Recommendations

**Proactive Token Refresh**: It is recommended to generate a new access token before the old one expires to ensure continuous access. This proactive approach helps in avoiding any service disruption due to token expiry.

**Buffer Period for Token Updates**: Clients should take advantage of the 6-hour validity window for old tokens after a refresh to ensure that the new tokens are updated across all services without immediate invalidation. This buffer period helps in synchronizing token updates across distributed systems.

> **Notes**  
> To avoid unexpected access issues, plan token refreshes considering the 10-token cap and the additional 6-hour window for old token validity.
>
> Ensure that your token refresh logic accommodates the possibility of old tokens being invalidated after the 6-hour window or if the 10-token limit is reached.
