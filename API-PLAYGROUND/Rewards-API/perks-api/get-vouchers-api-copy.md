---
title: "Fetch Offers API"
slug: "get-vouchers-api-copy"
excerpt: "Fetch Offers API enables the user to get a list of Offers with desired filters available with the Xoxoday catalog"
hidden: false
createdAt: "Tue Dec 24 2024 07:44:13 GMT+0000 (Coordinated Universal Time)"
updatedAt: "Tue Dec 23 2025 13:51:37 GMT+0000 (Coordinated Universal Time)"
openapi: "API-PLAYGROUND/Rewards-API/perks-api/spec.yaml POST /fetchOffers"
---
## List of available filters

| **Filter name** | **Functionality**                                   |
| :-------------- | :-------------------------------------------------- |
| country         | Users can filter products based on the country      |
| productName     | Users can filter products based on the product name |
| category        | Users can filter products based on the categoy      |

## Request Parameter

| **Parameter**   | **Type**        | **Description**                                                                      |
| :-------------- | :-------------- | :----------------------------------------------------------------------------------- |
| limit           | Int             | Number of results to return per page (used for pagination).                          |
| page            | Int             | Page number of results to fetch when using pagination.                               |
| includeProducts | String          | Comma-separated list of product IDs to explicitly include in the response.           |
| excludeProducts | String          | Comma-separated list of product IDs to explicitly exclude from the response.         |
| sort            | SortData        | Sorting configuration                                                                |
| sort.field      | String          | The field name to sort by.                                                           |
| sort.order      | String          | Sorting order → "ASC" for ascending or "DESC" for descending.                        |
| filters         | Array of Object | List of filters to apply. Each filter object should contain a **key** and **value**. |
| filters.key     | String          | The filter key                                                                       |
| filters.value   | String          | The filter value corresponding to the key                                            |

## Response Schema

| **Path**                                                | **Type**      | **Description**                        |
| ------------------------------------------------------- | ------------- | -------------------------------------- |
| data                                                    | object        | Root object.                           |
| data.getVouchers                                        | object        | Container for perk data.               |
| data.getVouchers.status                                 | number        | Status of request.                     |
| data.getVouchers.data                                   | array         | List of perks.                         |
| data.getVouchers.data\[].productId                      | number        | Unique product/perk ID.                |
| data.getVouchers.data\[].name                           | string        | Perk name.                             |
| data.getVouchers.data\[].description                    | string (HTML) | Description of the perk.               |
| data.getVouchers.data\[].termsAndConditionsInstructions | string (HTML) | T&C details.                           |
| data.getVouchers.data\[].expiryAndValidity              | string (HTML) | Expiry/validity info.                  |
| data.getVouchers.data\[].redemptionInstructions         | string (HTML) | Redemption steps.                      |
| data.getVouchers.data\[].categories                     | string        | Category name.                         |
| data.getVouchers.data\[].lastUpdateDate                 | string        | Last updated timestamp.                |
| data.getVouchers.data\[].imageUrl                       | string        | Perk image URL.                        |
| data.getVouchers.data\[].currencyCode                   | string        | Currency code.                         |
| data.getVouchers.data\[].currencyName                   | string        | Currency name.                         |
| data.getVouchers.data\[].countryName                    | string        | Country applicable.                    |
| data.getVouchers.data\[].countryCode                    | string        | ISO country code.                      |
| data.getVouchers.data\[].countries                      | array         | Applicable countries.                  |
| data.getVouchers.data\[].countries\[].code              | string        | ISO code.                              |
| data.getVouchers.data\[].countries\[].name              | string        | Country name.                          |
| data.getVouchers.data\[].valueType                      | string        | Always `fixed_denomination` for perks. |
| data.getVouchers.data\[].maxValue                       | number        | Max value (zero for perks).            |
| data.getVouchers.data\[].minValue                       | number        | Min value.                             |
| data.getVouchers.data\[].valueDenominations             | string        | Values (often `0`).                    |
| data.getVouchers.data\[].tatInDays                      | string        | Delivery time.                         |
| data.getVouchers.data\[].usageType                      | string        | `online`, `offline`, `both`.           |
| data.getVouchers.data\[].deliveryType                   | string        | `realtime`                             |
| data.getVouchers.data\[].orderQuantityLimit             | number        | Max allowed quantity.                  |
| data.getVouchers.data\[].isRecommended                  | number        | Recommended flag.                      |
| data.getVouchers.data\[].filterGroupCode                | string        | `offer_category` for perks.            |
| data.getVouchers.data\[].isPhoneNumberMandatory         | boolean       | Whether phone number is required.      |
| data.getVouchers.data\[].fee                            | number        | Any fee applied.                       |
| data.getVouchers.data\[].discount                       | number        | Discount if any.                       |
| data.getVouchers.data\[].metadata                       | object        | Perk-specific data block.              |
| data.getVouchers.data\[].metadata.categorytype          | string        | Always `offers`.                       |
| data.getVouchers.data\[].metadata.type                  | string        | Perk type (`code`/`link`).             |
| data.getVouchers.data\[].metadata.code                  | string        | Promo code (if available).             |
| data.getVouchers.data\[].metadata.link                  | string        | Redirect link.                         |
| data.getVouchers.data\[].metadata.expiryDate            | string        | Expiry date.                           |

## Implementation Notes

1. Read the "metadata" field in the `Fetch Offers API` response to get the Offer information like, 
   1. Code
   2. Link 
   3. Expiry Date of the Code / Link 
2. We recommend you cache the response from `Fetch Offers API` in your database every time you sync our catalog

> Learn about [Error Handling](https://dash.readme.com/project/xoxoday/v1.2/docs/error-handling-1), [Rate limiting](https://dash.readme.com/project/xoxoday/v1.2/docs/rate-limiting) and [Best Practice](https://dash.readme.com/project/xoxoday/v1.2/docs/concepts-1) .
