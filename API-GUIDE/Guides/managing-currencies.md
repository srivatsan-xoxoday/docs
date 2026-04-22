---
title: "Managing Cross-Currency Products"
slug: "managing-currencies"
excerpt: "Daily Exchange Rate for Cross-Currency Products"
hidden: false
createdAt: "Sun Aug 10 2025 15:28:48 GMT+0000 (Coordinated Universal Time)"
updatedAt: "Mon Apr 06 2026 10:02:38 GMT+0000 (Coordinated Universal Time)"
---
The system displays the applicable daily exchange rate for products based on your account’s base currency.

### Why this matters:

If your account’s base currency differs from the product’s currency, you’ll now know the exact amount you’ll be charged before placing the order—bringing clarity and transparency to your transactions.

### Example

| Parameter                  | Details      |
| :------------------------- | :----------- |
| **Customer Base Currency** | USD          |
| **Product Name**           | Starbucks UK |
| **Product Currency**       | GBP          |
| **Product Denomination**   | GBP 25       |
| **Exchange Rate Date**     | 10-08-2025   |
| **Exchange Rate Applied**  | 1.28         |
| **Order Amount (1 Qty)**   | USD 32.00    |

## Explanation:

If your account’s base currency is USD and you purchase a product priced at GBP 25, the system will apply the locked daily exchange rate (1.28) to calculate your cost in USD. In this case, GBP 25 × 1.28 = USD 32.00.

## How this helps you:

1. Accurate cost visibility before purchas
2. Eliminates surprises during billin
3. Ensures transparency for finance and audit teams

### Daily Exchange Rate Sync

1. Exchange rates are fetched from [Currencylayer](https://currencylayer.com/).
2. Rates are locked daily at 12:30 AM IST (06:31 PM UTC of the previous day)
3. The locked rate applies to all cross-currency orders placed until the next update.
