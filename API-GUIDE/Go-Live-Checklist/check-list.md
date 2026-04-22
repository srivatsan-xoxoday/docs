---
title: "Check List"
slug: "check-list"
excerpt: ""
hidden: false
createdAt: "Mon Aug 18 2025 06:09:06 GMT+0000 (Coordinated Universal Time)"
updatedAt: "Tue Aug 19 2025 11:00:33 GMT+0000 (Coordinated Universal Time)"
---
### Access & Security Setup

1. Provide access of the live environment to required developers.
2. Create unique user profiles for each team member.
3. Assign roles/permissions as per responsibilities.
4. Share IP addresses with Xoxoday for whitelisting.(Optional)
5. Enable two-factor authentication (2FA) for all users.(Optional)

### Wallet & Funds Management

1. Recharge the Xoxoday virtual wallet with sufficient funds for expected usage.
2. Verify funds reflect in the live wallet.
3. Configure low-balance alerts/notifications.
4. Define an internal process for wallet top-ups.

### API Authentication Setup

1. Obtain live client credentials (Client ID & Secret).
2. Generate access token successfully in the live environment.
3. Update integration to use live API base URLs (not sandbox).
4. Confirm Authorization headers are passed correctly in all API calls.

### Webhook Configuration

1. Register live webhook endpoints in the Xoxoday dashboard.
2. Ensure your server is publicly accessible and secured (HTTPS).
3. Validate system acknowledgment (200 OK) to prevent duplicate webhook retries.

Test webhook events:

1. Order status updates

### Functional Validation

1. Perform a test disbursement in live mode (with small denomination).
2. Verify recipient receives reward email/SMS successfully.
3. Confirm reporting/transaction logs reflect the test order.
4. Ensure error handling and retries are working in your system.

### Final Readiness Checks

1. Confirm campaigns and catalogs are correctly set up in live.
2. Double-check expiry, denominations, and country configurations.
3. Document support contacts and escalation path for live issues.
