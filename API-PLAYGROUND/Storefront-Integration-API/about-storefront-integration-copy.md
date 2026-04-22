---
title: "About Storefront Integration (COPY)"
slug: "about-storefront-integration-copy"
excerpt: "This article briefly introduces Xoxoday's Storefront Integration"
createdAt: "Tue Aug 26 2025 09:50:36 GMT+0000 (Coordinated Universal Time)"
updatedAt: "Tue Aug 26 2025 09:50:37 GMT+0000 (Coordinated Universal Time)"
hidden: true
---

# Marketplace Integration

With Xoxoday's Strorefront Integration, you can simply allow your users to be re-directed into Xoxoday's storefront/ marketplace.  Here you can simply provide SSO (Single Sign On) or SAML based authentication for your users to seamlessly login into Xoxoday's hosted Storefront.

Below are the advantages the **_Storefront integration_** has to offer that you may want to consider:

1. Use your platforms's native points engine to distribute points, while simply re-directing users onto Xoxoday's hosted Storefront to '_burn_' their accrued points.
2. A simple SSO or SAML based authentication to provide your users with a seamless access to storefornt.

Once users land in the storefront, our system will consume your end-points to `GET` points accrued in your system, and as well as `POST` back the points spent (by users) on their reward catalog.

# Below are the API Endpoints that Xoxoday will consume.

Note: Below APIs are to be provided by the client.

## Get Balance API:

Xoxoday will consume this API endpoint to fetch employees’ accrued points available for redemption (along with the currency unit).

Method: `GET`

### Response Params

| Query Params | Sample Data | Required in Response | Desc |
| --- | --- | --- | --- |
| userId | jsmth23 | ✅ | UUID is a unique userID passed to Xoxoday during the SSO session, which Xoxoday will use to query with. |
| availableAmount | 8925.15 | ✅ | Available Points accrued by the user are available to be spent for redemptions. |
| Currency units | USD | ✅ | The currency of the points value of the above. |
| WalletID | Wellness Wallet {string} |  | This parameter is useful in case you have multiple wallets in your module that the end user accrues points.  For Example, something like a wellness wallet, and learning wallet, |

### Sample Response Body (Imp Params)

```Text json
{
			"userId":"jsmth23",  // a uniqueID of the user/employee.
			"walletId":"Wellness Wallet", //Optional, walletID if multiple wallets are involved.
			"availableAmount":"8925.15", //Points currency available to spend
			"currency":"USD" //currency unit of the available points currency
}
```

## UpdatePoints API:

Xoxoday will consume this API endpoint to post back the points spent by the user to place an order on the Xoxoday’s Marketplace.

Method: `POST`

### Sample Request Body

```json

{
XoxodayTransactionId : "1703475", // this is the orderID of Xoxoday
"totalOrderAmount" : "5", 
"currency" : "USD", 
"comments" : "", 
"products" : {
"quantity" : "1", 
"orderAmount" : "5",
"price" : "5" 
"productId" : "28618", 
"name" : "Applebee's_eGift", 
"category" : null, 
"description" : "", 
}
```

^^ Highlights only important parameters we send in a request.

> 👍 Xoxoday will send the points (totalOrderAmount)\_ and additionally orderDetails, along with ProductDetails.

### Sample Response Body

```json
"TxnID" : "531661", //this is a Txn ID generated at your end that Xoxoday will persist to be used for RefundAPI 
```

> 👍 About TXNID
>
> TransactionID is something Xoxoday will persist on our end, and will be used to refund (if need be in the future) for reversal/refund of points.
>
> You can opt to store the Xoxoday orderID if you do not wish to generate a new ID on your side.

## GetProfile API:

Xoxoday will consume this API endpoint to validate user details(including points & user’s identity) during checkout to add an additional layer of security.

Method: `GET`

### Response Params

| Query Params | Sample Data | Required in Response | Desc |
| --- | --- | --- | --- |
| UUID | jsmth23 | ✅ | UUID is a unique userID passed to Xoxoday during the SSO session, which Xoxoday will use to query with. |
| firstName | John | ✅ | First Name of the user |
| lastName | Smith | ✅ | Last Name of the User |
| email address | [user@email.com](mailto:user@email.com) | ✅ | email address of the user |
| Country | United States |  | Country data field or equivalent from HRMS. |
| Phone Number | \+1 415342234 |  | Phone number of the employee |

### Sample Response Body

```json
{
        "userId": "cgrant1",
        "firstName": "Carla",
        "lastName": "Grant",
        "country": "United States",
        "email": "carla@company.com",   
				"phone": "+1 415342234",
 }
```

^^Highlights only important parameters we expect.

> 📘 Xoxoday can consume the FetchPoints API itself for profile information as well, if the  information we need to validate identity are available in the response

## RefundAPI:

Xoxoday will consume this API to refund back the user’s points, in the rare case, when Xoxoday is unable to fulfill an order.

Method: `POST`

### Request body

```json
'{
    "TxnID": "531661", //your system txn ID that we persist(ed)
    "currency":"USD",
    "userId":"sfadmin",
    "refundAmount":"1",
    "vendor":"XOXODAY"
}'
```

^^Highlights one important parameter we send in a request.

# All Xoxoday's requests are sent from the following IP addresses:

> 🚧 ## All Xoxoday requests are sent from the following IP addresses:
>
> Staging:
>
> - 50.112.248.135
> - 54.184.56.156
> - 52.24.158.163
> - 34.217.113.26
> - 54.185.176.191
>
> Production :
>
> - 52.76.120.90
> - 52.74.39.101
> - 52.221.42.47
> - 46.137.196.217

> 🚧 ## All Xoxoday requests are sent from the following domain(s):
>
> Staging:
>
> - [https://canvas.xoxoday.com](https://canvas.xoxoday.com)
> - [https://canvas.xoxoday.com](https://canvas.xoxoday.com)
> - [https://canvas.plum.gift](https://canvas.plum.gift)
>
> Production:
>
> - [https://stores.xoxoday.com](https://stores.xoxoday.com)
> - [https://accounts.xoxoday.com](https://accounts.xoxoday.com)
> - [https://app.xoxoday.com](https://app.xoxoday.com)
> - [https://plum.gift](https://plum.gift)