---
title: "Error Handling"
slug: "error-handling-1"
excerpt: "In this section, you'll find all the conventional HTTP error codes associated with Xoxoday's Rewards APIs."
hidden: false
createdAt: "Mon Aug 11 2025 07:38:35 GMT+0000 (Coordinated Universal Time)"
updatedAt: "Tue Aug 19 2025 11:00:16 GMT+0000 (Coordinated Universal Time)"
---
The Xoxoday Rewards APIs use standard HTTP status codes to indicate whether a request was successful or failed.

1. 2xx codes → Successful requests
2. 4xx or 5xx codes → Failed requests

When a request fails, the API returns an error response in JSON format containing specific attributes.

## Error Response Formats

The API can return errors in two possible formats:

### OAuth / Authorization Errors

Returned when authentication or authorization fails, or when required parameters are missing.

**Attributes**:

```json
{  
  "error": "invalid_request",  
  "error_description": "missing/invalid parameters authorization header"  
}
```

**Attribute	Description**

| Attribute           | Description                                                                                          |
| :------------------ | :--------------------------------------------------------------------------------------------------- |
| `error`             | A short error keyword describing the type of error (e.g., `invalid_request`, `unauthorized_client`). |
| `error_description` | A detailed explanation of the error.                                                                 |

### Application / API Errors

Returned when a valid request was made, but the server could not process it due to resource, business logic, or data issues.

<br />

**Attributes**:

```json
{  
  "code": 404,  
  "errorId": "PLE10030",  
  "errorInfo": "Failed to find vouchers.",  
  "error": "No Vouchers Found"  
}
```

**Attribute	Description**

| Attribute     | Description                                                                   |
| :------------ | :---------------------------------------------------------------------------- |
| **code**      | The HTTP status code returned. Possible categories: 2xx, 4xx, 5xx             |
| **errorId**   | A short string describing the type of error (selected from a predefined list) |
| **errorInfo** | A short description of the error                                              |
| **error**     | Additional details explaining the cause of the error                          |

### Standard HTTP Error Code Summary

| HTTP Status Code | Text                   | Description                                                                                      |
| :--------------- | :--------------------- | :----------------------------------------------------------------------------------------------- |
| **400**          | Bad Request            | The request was invalid. Common causes: malformed JSON or rule violation.                        |
| **401**          | Unauthorized           | Authorization failed or was not provided.                                                        |
| **404**          | Not Found              | The requested resource does not exist.                                                           |
| **405**          | Method Not Allowed     | The HTTP method is recognized but disabled. _(GET and HEAD must always be enabled)_              |
| **406**          | Not Acceptable         | No content matches the criteria provided in the request headers.                                 |
| **415**          | Unsupported Media Type | The request’s media type is not supported by the server.                                         |
| **500**          | Internal Server Error  | Server-side issue. Contact **[cs@xoxoday.com](mailto:cs@xoxoday.com)** for immediate resolution. |

> **Note**  
> All other HTTP status codes follow their standard meanings as defined in the HTTP specification.  
> Refer to: MDN HTTP Status Codes

### Error Related to APIs

Some other common errors related to the Rewards APIs are listed below:

| No. | Error Code | Description                                           | API Endpoints                              | HTTP Status Code | Actions                                                                                                                                                         |
| :-- | :--------- | :---------------------------------------------------- | :----------------------------------------- | :--------------- | :-------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| 1   | PLE10001   | Validation error in place order                       | PlaceOrder                                 | HTTP400          | Please check the json payload.                                                                                                                                  |
| 2   | PLE10002   | Validation error in get order details                 | GetorderDetails, GetorderHistory           | HTTP400          | Please check the json payload.                                                                                                                                  |
| 3   | PLE10003   | Validation error in get filters                       | GetFilters                                 | HTTP400          | Please check the json payload.                                                                                                                                  |
| 4   | PLE10004   | Failed to validate client's externalOrderId           | GetOrderHistory                            | HTTP422          | The validation of poNumber has failed.                                                                                                                          |
| 5   | PLE10005   | Failed to get currency value                          | PlaceOrder                                 | HTTP502          | Please try again after sometime.                                                                                                                                |
| 6   | PLE10006   | Invalid response from currency API                    | PlaceOrder                                 | HTTP502          | Please try again after sometime.                                                                                                                                |
| 7   | PLE10007   | Failed to add order                                   | PlaceOrder                                 | HTTP422          | Order placement failed. Call the PlaceOrder API again.                                                                                                          |
| 8   | PLE10008   | Failed to get Order Amount details                    | GetOrderHistory                            | HTTP502          | Please contact [cs@xoxoday.com](mailto:cs@xoxoday.com)                                                                                                          |
| 9   | PLE10009   | Failed to get company points                          | Getbalance                                 | HTTP502          | Please contact [cs@xoxoday.com](mailto:cs@xoxoday.com)                                                                                                          |
| 10  | PLE10010   | Failed to redeem points                               | PlaceOrder                                 | HTTP422          | Order placement failed. Call the PlaceOrder API again.                                                                                                          |
| 11  | PLE10011   | Failed to confirm order                               | PlaceOrder                                 | HTTP422          | Order placement failed. Call the PlaceOrder API again.                                                                                                          |
| 12  | PLE10012   | Failed to process order                               | PlaceOrder                                 | HTTP502          | Order placement failed. Call the PlaceOrder API again.                                                                                                          |
| 13  | PLE10013   | Failed to confirm points redeemed                     | GetVoucher,GetOrderDetials,GetorderHistory | HTTP503          | Please contact [cs@xoxoday.com](mailto:cs@xoxoday.com)                                                                                                          |
| 14  | PLE10014   | Invalid client                                        | PlaceOrder                                 | HTTP400          | Please contact [cs@xoxoday.com](mailto:cs@xoxoday.com)                                                                                                          |
| 15  | PLE10015   | Amazon KYC is not approved                            | PlaceOrder                                 | HTTP400          | Amazon KYC process is not done. Please contact [cs@xoxoday.com](mailto:cs@xoxoday.com)                                                                          |
| 16  | PLE10016   | Failed to get Order details                           | GetorderDetails                            | HTTP404          | Order ID or poNumber passed is incorrect.                                                                                                                       |
| 17  | PLE10017   | Failed to get product details                         | GetVoucher                                 | HTTP404          | Product details are not available. Please refresh the catalog by calling getvouchers API every 24 hours.                                                        |
| 18  | PLE10018   | Invalid denomination for the product                  | PlaceOrder                                 | HTTP400          | The denomination passed is not valid. Please check and pass correct denomination from GetVoucher API.                                                           |
| 19  | PLE10019   | Clients are not allowed to place international orders | PlaceOrder                                 | HTTP401          | International products are disabled. Please write to [cs@xoxoday.com](mailto:cs@xoxoday.com) to enable it.                                                      |
| 20  | PLE10020   | Failed to get currency details for the client         | PlaceOrder                                 | HTTP404          | Please try again after sometime.                                                                                                                                |
| 21  | PLE10021   | Failed to find order details while fulfilling order   | GetOrderDetails                            | HTTP404          | Please try again after sometime.                                                                                                                                |
| 22  | PLE10022   | Failed to find order history                          | GetOrderHistory                            | HTTP404          | Order ID or poNumber passed is incorrect.                                                                                                                       |
| 23  | PLE10023   | Failed to get client's balance                        | GetBalance                                 | HTTP502          | Please check the json payload.                                                                                                                                  |
| 24  | PLE10024   | Vouchers are out of stock                             | PlaceOrder                                 | HTTP502          | Stock will be replenish. Please try again after sometime.                                                                                                       |
| 25  | PLE10025   | Failed to place order for the client                  | Placeorder                                 | HTTP502          | System could not place the order. Please try again after sometime.                                                                                              |
| 26  | PLE10026   | Order cancelled but refund failed                     | PlaceOrder                                 | HTTP404          | Please write to [cs@xoxoday.com](mailto:cs@xoxoday.com)                                                                                                         |
| 27  | PLE10027   | Failed to find order history                          | GetorderHistory                            | HTTP404          | Order ID or poNumber passed is incorrect.                                                                                                                       |
| 28  | PLE10028   | Failed to find TransactionId                          | \*\*\*                                     | HTTP404          | Order ID or poNumber passed is incorrect.                                                                                                                       |
| 29  | PLE10029   | Failed to find filters for filterGroupCode            | GetFilters                                 | HTTP404          | The filter Group code used is invalid. Please check the value code in GetFilters API.                                                                           |
| 30  | PLE10030   | Failed to find vouchers                               | GetVouchers                                | HTTP404          | Please try again after some time.                                                                                                                               |
| 31  | PLE10031   | Invalid filter value code                             | GetVouchers                                | HTTP400          | The filter value code used is invalid. Please check the value code in GetFilters API.                                                                           |
| 32  | PLE10032   | Failed to validate OrderHistory Request               | GetorderHistory                            | HTTP400          | Please check the json payload.                                                                                                                                  |
| 33  | PLE10033   | Failed to validate getVouchers request                | GetVoucher                                 | HTTP400          | Please check the json payload.                                                                                                                                  |
| 34  | PLE10034   | Failed to process resendVoucher                       | GetOrderDetails                            | HTTP502          | GetOrderDetails API failed to resend the voucher details. Please try again after sometime.                                                                      |
| 35  | PLE10035   | Failed to get order details to check status of order  | PlaceOrder                                 | HTTP502          | PlaceOrder API has failed to check the status of the order. Please call the GetOrderDetails API and pass the same poNumber.                                     |
| 36  | PLE10036   | Failed to get order details as delivery is canceled.  | PlaceOrder                                 | HTTP404          | Order delivery is in cancelled state.                                                                                                                           |
| 37  | PIPE10015  | Plum Pro APIs: User is disabled                       | \*\*\*                                     | HTTP401          | Please contact [cs@xoxoday.com](mailto:cs@xoxoday.com)                                                                                                          |
| 38  | PIPE10016  | Plum Pro APIs: Company is disabled                    | \*\*\*                                     | HTTP401          | Please contact [cs@xoxoday.com](mailto:cs@xoxoday.com)                                                                                                          |
| 39  | PIPE10017  | Plum Pro APIs: Access restricted for this IP          | \*\*\*                                     | HTTP401          | IP must have blacklisted. Please share your server IP to [cs@xoxoday.com](mailto:cs@xoxoday.com) and get it whitelisted.                                        |
| 41  | PLE10041   | Clients are not allowed to place more than 10 Qty     | PlaceOrder                                 | HTTP409          | In an order, maximum ordered quantity of any product cannot exceed more than 9999. Please divide the order into smaller chunks and call the API multiple times. |
| 42  | PLE10042   | This product is not activated for the client.         | PlaceOrder                                 | HTTP404          | This product is disabled, please submit your KYB. In case already done, please contact [cs@xoxoday.com](mailto:cs@xoxoday.com).                                 |
