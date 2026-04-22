---
title: "Set Up Your Environment"
slug: "set-up-your-environment-copy"
excerpt: "Xoxoday offers two API environments: Sandbox for testing, and Production for live reward processing.  Understanding how these environments work helps ensure a smooth integration experience — from initial testing to full-scale deployment."
hidden: false
createdAt: "Sun Aug 17 2025 11:32:48 GMT+0000 (Coordinated Universal Time)"
updatedAt: "Fri Oct 24 2025 07:28:03 GMT+0000 (Coordinated Universal Time)"
---
## Sandbox Environment

The Sandbox environment is designed for development and testing. It simulates reward flows using test data and test balances — so you can experiment safely without triggering real transactions or incurring any costs.

1. No KYC or funding required
2. Test balance and mock reward products
3. Safe to test authentication, order flows, and error handling
4. Great for building and validating your integration

Use this to prototype, test, and refine your implementation before going live.

## Production Environment

The Production environment is used for live reward delivery. Any API requests here will result in real transactions and will deduct from your wallet balance.

1. Requires business verification (KYB) and wallet funding
2. Access to real catalog, live inventory, and true recipient experiences

Used when you're ready to go live with your customers or users

Only move to production once your flows are fully tested in sandbox.

Selecting an Environment  
Each environment has its own base URL and API key type:

| Environment | Base URL                                              |
| :---------- | :---------------------------------------------------- |
| Sandbox     | https://stagingstores.xoxoday.com/chef/v1/oauth/api |
| Production  | https://accounts.xoxoday.com/chef/v1/oauth/api    |

Be sure to use the appropriate URL and API key for the environment you’re working in.

### Sandbox Limitations

While the sandbox mimics production behavior closely, a few differences existll delivered rewards are dummy.

Always test in sandbox, but validate final flows in production with low-value test transactions where needed.
