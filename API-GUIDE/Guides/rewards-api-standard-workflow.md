---
title: "Xoxoday API — Standard Workflow & Example"
slug: "rewards-api-standard-workflow"
excerpt: "A practical guide showing how developers can integrate with Xoxoday’s core APIs in the correct sequence, including endpoint purpose, example requests, responses, and integration flow."
hidden: false
createdAt: "Tue Nov 04 2025 17:52:40 GMT+0000 (Coordinated Universal Time)"
updatedAt: "Mon Nov 24 2025 14:02:37 GMT+0000 (Coordinated Universal Time)"
---
## Authentication & Common Headers

All API calls require an Authorization header and standard headers:

```
Authorization: Bearer {ACCESS_TOKEN}
Content-Type: application/json
```

To generate the access token, authenticate using Xoxoday’s OAuth API. You can refer to the [documentation here](https://developers.xoxoday.com/docs/create-your-api-key).

***

## Core APIs

1. **Get Filters API** — Retrieves available filters like country, brand, and category for the voucher catalog.
2. **Get Vouchers API** — Fetches voucher list based on filters and country.
3. **Get Balance API** — Returns wallet balance for the authenticated client.
4. **Place Order API** — Places an order for selected vouchers.
5. **Get Order Details API** — Fetches order details for a given order ID or PO number.
6. **Get Order History API** — Lists all orders placed within a given timeframe.
7. **Get Payment Report API** — Provides a detailed payment report for reconciliation.

***

## Workflow Diagram

![](https://files.readme.io/fae625031c34f8a197b28e16e6e7dc3de0e866ee7029d5d321b01de27f438d8a-Group_1_1.png)

<br />

***

## Standard Workflow — From Browse to Redemption

### Retrieve Filters

**Purpose:** Get the filters for vouchers (country, brand, category).

**Example Request:**

```bash
curl --request POST \
     --url https://stagingstores.xoxoday.com/chef/v1/oauth/api \
     --header 'accept: application/json' \
     --header 'content-type: application/json' \
     --data '
{
  "query": "plumProAPI.mutation.getFilters",
  "tag": "plumProAPI",
  "variables": {
    "data": {
      "filterGroupCode": "Country",
      "includeFilters": "",
      "excludeFilters": "uae"
    }
  }
}
```

**Example Response:**

```json
{
  "data": {
    "getFilters": {
      "status": 1,
      "data": [
        {
          "filterGroupName": "Country",
          "filterGroupDescription": "",
          "filterGroupCode": "country",
          "filters": [
            {
              "filterValue": "Afghanistan",
              "isoCode": "AF",
              "filterValueCode": "afghanistan"
            },
            {
              "filterValue": "Andorra",
              "isoCode": "AD",
              "filterValueCode": "andorra"
            }
          ]
        }
      ]
    }
  }
}
```

***

### Retrieve Vouchers

**Purpose:** Get vouchers available for the selected country and filters.

**Example Request:**

```bash
curl --request POST \
     --url https://stagingstores.xoxoday.com/chef/v1/oauth/api/ \
     --header 'accept: application/json' \
     --header 'content-type: application/json' \
     --data '
{
  "query": "plumProAPI.mutation.getVouchers",
  "tag": "plumProAPI",
  "variables": {
    "data": {
      "limit": 10,
      "page": 1,
      "includeProducts": "",
      "excludeProducts": "",
      "exchangeRate": 1,
      "sort": {
        "field": "name",
        "order": "ASC"
      }
    }
  }
}
'
```

**Example Response:**

```json
{
  "data": {
    "getVouchers": {
      "status": 1,
      "data": [
        {
          "productId": 1535,
          "name": "Amazon.in",
          "description": "",
          "orderQuantityLimit": 10,
          "termsAndConditionsInstructions": "",
          "expiryAndValidity": "",
          "redemptionInstructions": "",
          "categories": "eCommerce",
          "lastUpdateDate": "2020-01-06 10:23:24",
          "imageUrl": "",
          "currencyCode": "INR",
          "currencyName": "rupees",
          "countryName": "India",
          "countryCode": "IN",
          "countries": [
            {
              "code": "IN",
              "name": "India"
            }
          ],
          "valueType": "fixed_denomination",
          "maxValue": 0,
          "minValue": 0,
          "valueDenominations": "20,30,500,1000,2500",
          "tatInDays": 0,
          "usageType": "",
          "deliveryType": "",
          "isCommon": "",
          "fee": 0,
          "discount": 0,
          "exchangeRate": "1",
          "isPhoneNumberMandatory": false,
          "isRecommended": 1,
          "filterGroupCode": "voucher_category"
        }
      ]
    }
  }
}
```

***

### Get Balance

**Purpose:** Fetch available wallet balance before placing an order.

**Example Request:**

```bash
curl --request POST \
     --url https://stagingstores.xoxoday.com/chef/v1/oauth/api \
     --header 'accept: application/json' \
     --header 'content-type: application/json' \
     --data '
{
  "query": "plumProAPI.query.getBalance",
  "tag": "plumProAPI",
  "variables": {
    "data": {}
  }
}
'
```

**Example Response:**

```json
{
  "data": {
    "getBalance": {
      "status": 1,
      "data": {
        "value": 5870.02,
        "currency": "INR"
      }
    }
  }
}
```

**Usage:** If balance \< voucher price, notify the user to top-up before placing an order.

***

### Place Order

**Purpose:** Call place order API to procure a voucher.

**Example Request:**

```bash
curl --request POST \
     --url https://stagingstores.xoxoday.com/chef/v1/oauth/api/ \
     --header 'accept: application/json' \
     --header 'content-type: application/json' \
     --data '
{
  "query": "plumProAPI.mutation.placeOrder",
  "tag": "plumProAPI",
  "variables": {
    "data": {
      "productId": 15365,
      "quantity": 1,
      "denomination": 20,
      "email": "your.email@example.com",
      "contact": "+1-4705000000",
      "tag": "Rewarding",
      "poNumber": "PO12662",
      "notifyReceiverEmail": 0,
      "notifyAdminEmail": 0
    }
  }
}
'
```

**Example Response:**

```json
{
  "data": {
    "placeOrder": {
      "status": 1,
      "data": {
        "orderId": 6474256,
        "orderTotal": 100,
        "orderDiscount": "",
        "discountPercent": "",
        "currencyCode": "INR",
        "currencyValue": 1,
        "amountCharged": 100,
        "orderStatus": "complete",
        "deliveryStatus": "delivered",
        "tag": "",
        "quantity": 1,
        "vouchers": [
          {
            "productId": 1007,
            "orderId": 6474256,
            "voucherCode": "DEMO-1676340039265-p6aqnl",
            "pin": "DEMO-PIN",
            "validity": "2028-02-14",
            "amount": 100,
            "currency": "INR",
            "country": "IN",
            "type": "codePin",
            "currencyValue": 1
          }
        ],
        "voucherDetails": [
          {
            "orderId": 6474256,
            "productId": 1007,
            "productName": "Flipkart",
            "currencyCode": "INR",
            "productStatus": "delivered",
            "denomination": 100
          }
        ]
      }
    }
  }
}
```

***

### Get Order Details

**Purpose:** Retrieve the details and status of an order.

**Example Request:**

```bash
curl --request POST \
     --url https://stagingstores.xoxoday.com/chef/v1/oauth/api \
     --header 'accept: application/json' \
     --header 'content-type: application/json' \
     --data '
{
  "query": "plumProAPI.mutation.getOrderDetails",
  "tag": "plumProAPI",
  "variables": {
    "data": {
      "poNumber": "PO123",
      "orderId": 123,
      "sendMailToReceiver": 0
    }
  }
}
'
```

**Example Response:**

```json
{
  "data": {
    "getOrderDetails": {
      "status": 1,
      "data": {
        "orderId": 1,
        "vouchers": [
          {
            "amount": "10",
            "country": "India",
            "currency": "INR",
            "orderId": 128618,
            "pin": "key_c26323726135beaa4e",
            "productId": 28543,
            "tag": "somethingToTagThisOrder",
            "type": "codePin",
            "validity": "2020-10-02",
            "voucherCode": "4162581029814703",
            "currencyValue": 0.1
          }
        ],
        "amountCharged": 90,
        "currencyCode": "USD",
        "discountPercent": 10,
        "orderDiscount": 10,
        "orderTotal": 100,
        "orderStatus": "complete",
        "deliveryStatus": "pending"
      }
    }
  }
}
```

***

### Get Order History

**Purpose:** List all past orders placed by the client.

**Example Request:**

```bash
curl --request POST \
     --url https://stagingstores.xoxoday.com/chef/v1/oauth/api \
     --header 'accept: application/json' \
     --header 'content-type: application/json' \
     --data '
{
  "query": "plumProAPI.mutation.getOrderHistory",
  "tag": "plumProAPI",
  "variables": {
    "data": {
      "startDate": "2012-07-25",
      "endDate": "2012-07-28",
      "limit": 10,
      "page": 1
    }
  }
}
'
```

**Example Response:**

```json
{
  "data": {
    "getOrderDetails": {
      "status": 1,
      "data": {
        "orderId": 6474256,
        "orderTotal": 100,
        "orderDiscount": "",
        "discountPercent": "",
        "currencyCode": "INR",
        "currencyValue": 1,
        "amountCharged": 100,
        "orderStatus": "complete",
        "deliveryStatus": "delivered",
        "tag": "",
        "orderDate": "2024-02-07 12:25:45",
        "quantity": 1,
        "shippingDetails": {
          "shippingFirstName": "",
          "shippingLastName": "",
          "shippingContactNo": "",
          "shippingCompany": "",
          "shippingAddress1": "",
          "shippingAddress2": "",
          "shippingCity": "",
          "shippingState": "",
          "shippingCountry": "",
          "shippingPostcode": ""
        },
        "vouchers": [
          {
            "productId": 1007,
            "orderId": 6474256,
            "voucherCode": "DEMO-1676340039265-p6aqnl",
            "pin": "DEMO-PIN",
            "validity": "2028-02-14",
            "amount": 100,
            "currency": "INR",
            "country": "IN",
            "type": "codePin",
            "currencyValue": 1
          }
        ],
        "voucherDetails": [
          {
            "orderId": 6474256,
            "productId": 1007,
            "productName": "Flipkart",
            "currencyCode": "INR",
            "productStatus": "delivered",
            "denomination": 100
          }
        ]
      }
    }
  }
}
```

***

### Get Payment Report

**Purpose:** For admins to reconcile payments or settlements.

**Example Request:**

```bash
curl --request POST \
     --url https://stagingstores.xoxoday.com/chef/v1/oauth/api \
     --header 'accept: application/json' \
     --header 'content-type: application/json' \
     --data '
{
  "query": "plumProAPI.mutation.paymentHistory",
  "tag": "plumProAPI",
  "data": {
    "data": {
      "startDate": "2012-07-25",
      "endDate": "2012-07-28",
      "limit": 10,
      "page": 1
    }
  }
}
'
```

**Example Response:**

```json
{
  "data": {
    "getPaymentReport": {
      "status": 1,
      "data": [
        {
          "invoice_number": "N3352A",
          "reference_id": "zYEgsdgUTZA3",
          "date": "2023-06-01",
          "reason": "Brand vouchers issued",
          "adjusted_amount": 100,
          "transaction_status": "Complete",
          "closing_balance": 97690
        },
        {
          "invoice_number": "IN423204732",
          "reference_id": "778mM7etFj",
          "date": "2023-05-23",
          "reason": "Funds added",
          "adjusted_amount": 100000,
          "transaction_status": "Complete",
          "closing_balance": 100000
        }
      ]
    }
  }
}
```

<br />

> To explore the Rewards APIs in more detail and understand each endpoint thoroughly, please refer to the [Xoxoday Rewards API documentation](https://developers.xoxoday.com/reference/giftcard-api)
