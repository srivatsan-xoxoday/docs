---
title: "Rate Limiting"
slug: "rate-limiting"
excerpt: ""
hidden: false
createdAt: "Mon Aug 11 2025 08:10:33 GMT+0000 (Coordinated Universal Time)"
updatedAt: "Wed Jan 21 2026 06:39:14 GMT+0000 (Coordinated Universal Time)"
---
To maintain system performance and ensure fair usage for all clients, the following rate limits per minute apply to the Plum APIs:

### Rate Limits for each API (Per Minute)

1. **getOrderDetailsAPI**: 200 requests
2. **getVouchersAPI**: 50 requests
3. **getBalanceAPI**: 10 requests
4. **placeOrderAPI**: 100 requests
5. **getOrderHistoryAPI**: 200 requests
6. **getFiltersAPI**: 50 requests

When the limit for any API is crossed, the system returns the following response:

```json
{  
  "errors": [  
    {  
      "message": "auth.request_limit_exceeded",  
      "penaltySeconds": 60  
    }  
  ]  
}
```

<br />

### Recommendations

1. Spread out API calls to avoid hitting the per-minute threshold.
2. Cache responses for static or slow-changing data such as vouchers and filters.
3. Use retries with exponential backoff, respecting the penaltySeconds value before retrying.
