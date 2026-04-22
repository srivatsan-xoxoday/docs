---
title: "Mobile Top up"
slug: "mobile-top-up"
excerpt: ""
hidden: false
createdAt: "Fri Aug 22 2025 05:37:11 GMT+0000 (Coordinated Universal Time)"
updatedAt: "Tue Aug 26 2025 14:29:12 GMT+0000 (Coordinated Universal Time)"
---
### Where can we find the API catalog for Mobile Top-up?

1. You can explore our API documentation here:  
   👉 Mobile Top-up API Reference

### Does the Mobile Top-up API work differently for different countries?

1. No. It works the same way across all countries. However:
   1. Each operator has predefined fixed plans/packages.
   2. Custom recharge is not supported at the moment.
   3. The minimum recharge amount depends on the operator’s available plans.

### Can the operator be auto-identified from the user’s mobile number?

1. We are currently building this feature.
   1. For now, the user will need to select the operator manually.
   2. Once live, this will work the same across all countries.

### How does fulfillment of mobile recharge work?

1. The fulfillment flow is as follows:
   1. Authentication → Client authenticates with our APIs using provided credentials.
   2. Fetch Operators → Client calls the Get Mobile Top-up API to retrieve available operators for a country.
   3. Fetch Plans → Once an operator is selected, client calls the API again with the parentProductId to get available plans.
   4. User Input → End-user selects a plan and enters their mobile number.
   5. Place Order → Client calls the Place Order API with selected plan & number.
   6. Fulfillment → Recharge is processed instantly by the telecom provider.
   7. Confirmation:
      1. Client receives API success/failure response.
      2. End-customer receives SMS/notification directly from the operator.
      3. No additional action is required from the user.

### How does wallet balance work?

You will be required to maintain a wallet balance with us.

When you place an order:

1. If balance is sufficient → the order is processed.
2. If balance is low → the order request fails.

Postpaid billing is not supported.

### In case of delays or failures, how can we get support?

You can raise a ticket by emailing [cs@xoxoday.com](mailto:cs@xoxoday.com)  
.  
Our support team will provide quick resolution for such cases.

### Which countries does this API Supports?

Our Mobile Top-up API supports multiple countries, You can access our catalogue here: LINK

### Understanding Operators & Plans (Step-by-Step)

**Q1. How do we fetch the list of mobile operators for a country?**

You need to call the Get Mobile Top-up API with the country code.

1. Example: Passing country: IN will return a list of operators in India.

**Q2. How do we fetch recharge plans for an operator?**

1. Once you have the operator’s parentProductId (fetched in Step 1),
2. Call the Get Mobile Top-up API again, passing the parentProductId.
3. This will return all available recharge/top-up plans for that operator (with denominations).

**Q3. What do we need to place a recharge order?**

You will need:

1. productId (specific plan ID)
2. mobile number
3. quantity (usually 1)
4. denomination (value of the recharge)

Then call the Place Order API with these details.
