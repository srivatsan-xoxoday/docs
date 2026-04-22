---
title: "Get Lounge Catalog"
slug: "fetch-lounge-catalog"
excerpt: "With the Fetch Lounge Catalog API, you can retrieve a curated list of available lounges across the globe."
hidden: false
createdAt: "Thu Apr 10 2025 05:57:23 GMT+0000 (Coordinated Universal Time)"
updatedAt: "Sat Nov 22 2025 21:22:51 GMT+0000 (Coordinated Universal Time)"
openapi: "API-PLAYGROUND/Rewards-API/lounge/spec.yaml POST /getLoungesCatalog"
---
## Get Voucher API Schema

| **Parameter**   | **Type**        | **Description**                                                                      |
| :-------------- | :-------------- | :----------------------------------------------------------------------------------- |
| limit           | Int             | Number of results to return per page (used for pagination).                          |
| page            | Int             | Page number of results to fetch when using pagination.                               |
| includeProducts | String          | Comma-separated list of product IDs to explicitly include in the response.           |
| excludeProducts | String          | Comma-separated list of product IDs to explicitly exclude from the response.         |
| sort            | SortData        | Sorting configuration (e.g., by price, name, popularity).                            |
| sort.field      | String          | The field name to sort by (e.g., "name")                                             |
| sort.order      | String          | Sorting order → "ASC" for ascending or "DESC" for descending.                        |
| filters         | Array of Object | List of filters to apply. Each filter object should contain a **key** and **value**. |
| filters.key     | String          | The filter key (e.g., `country`, `currency`, `product_category`).                    |
| filters.value   | String          | The filter value corresponding to the key (e.g., `IN`, `USD`, `Electronics`).        |

## Filter Reference Table

| Key          | Value Type | Description                                       |
| :----------- | :--------- | :------------------------------------------------ |
| productName  | String     | Product names to be included                      |
| country      | String     | Countries to be included                          |
| price        | String     | Price range filters to be included                |
| minPrice     | String     | Minimum price of the products looked for          |
| maxPrice     | String     | Maximum price of the products looked for          |
| currencyCode | String     | Currency codes to be included                     |
| deliveryType | String     | Delivery type to the voucher (realtime or delayed |

## Response Schema

| **Path**                                                | **Type**      | **Description**                                                           |
| :------------------------------------------------------ | :------------ | :------------------------------------------------------------------------ |
| data                                                    | object        | Root response object.                                                     |
| data.getVouchers                                        | object        | Container for catalogue data.                                             |
| data.getVouchers.status                                 | number        | API execution status (`1` = success).                                     |
| data.getVouchers.data                                   | array         | List of voucher products.                                                 |
| data.getVouchers.data\[].productId                      | number        | Unique identifier for the voucher product.                                |
| data.getVouchers.data\[].name                           | string        | Product name.                                                             |
| data.getVouchers.data\[].description                    | string (HTML) | Description (supports HTML content).                                      |
| data.getVouchers.data\[].orderQuantityLimit             | number        | Maximum quantity allowed per order.                                       |
| data.getVouchers.data\[].termsAndConditionsInstructions | string (HTML) | Terms & conditions; may contain HTML and links.                           |
| data.getVouchers.data\[].brand                          | array         | Brand metadata (may be empty).                                            |
| data.getVouchers.data\[].expiryAndValidity              | string (HTML) | Voucher validity details.                                                 |
| data.getVouchers.data\[].redemptionInstructions         | string (HTML) | Instructions for redeeming the voucher.                                   |
| data.getVouchers.data\[].categories                     | string        | Comma-separated list of product categories.                               |
| data.getVouchers.data\[].lastUpdateDate                 | string        | Last update timestamp.                                                    |
| data.getVouchers.data\[].imageUrl                       | string        | Product image URL.                                                        |
| data.getVouchers.data\[].currencyCode                   | string        | Currency code.                                                            |
| data.getVouchers.data\[].currencyName                   | string        | Currency name.                                                            |
| data.getVouchers.data\[].countryName                    | string        | Country where product is redeemable.                                      |
| data.getVouchers.data\[].countryCode                    | string        | ISO country code.                                                         |
| data.getVouchers.data\[].countries                      | array         | List of redemption countries.                                             |
| data.getVouchers.data\[].countries\[].code              | string        | Country ISO code.                                                         |
| data.getVouchers.data\[].countries\[].name              | string        | Country name.                                                             |
| data.getVouchers.data\[].valueType                      | string        | Denomination type (`fixed_denomination`, `open_value`).                   |
| data.getVouchers.data\[].maxValue                       | number        | Maximum value (for open value vouchers).                                  |
| data.getVouchers.data\[].minValue                       | number        | Minimum value.                                                            |
| data.getVouchers.data\[].valueDenominations             | string        | Comma-separated fixed denominations.                                      |
| data.getVouchers.data\[].tatInDays                      | string        | Delivery turnaround time.                                                 |
| data.getVouchers.data\[].usageType                      | string        | `online`, `offline`, or `both`.                                           |
| data.getVouchers.data\[].deliveryType                   | string        | `realtime` or `delayed`.                                                  |
| data.getVouchers.data\[].fee                            | number        | Additional fee applied.                                                   |
| data.getVouchers.data\[].discount                       | number        | Discount applied.                                                         |
| data.getVouchers.data\[].exchangeRate                   | number        | FX conversion rate used.                                                  |
| data.getVouchers.data\[].isPhoneNumberMandatory         | boolean       | Whether phone number is required at checkout.                             |
| data.getVouchers.data\[].variants                       | array / null  | Product variants (if any).                                                |
| data.getVouchers.data\[].isRecommended                  | number        | Recommendation flag (`0` or `1`).                                         |
| data.getVouchers.data\[].filterGroupCode                | string        | Filter group identifier.                                                  |
| data.getVouchers.data\[].productMeta                    | string (JSON) | JSON structure defining dynamic checkout fields (e.g., email validation). |
| data.getVouchers.data\[].loyaltyName                    | string / null | Loyalty program name.                                                     |
| data.getVouchers.data\[].loyaltyConversion              | number / null | Conversion factor for loyalty points.                                     |
| data.getVouchers.data\[].metaData                       | string / null | Additional metadata.                                                      |
| data.getVouchers.data\[].showDiscountPercent            | number        | Whether discount percent should be displayed.                             |
| data.getVouchers.data\[].productImages                  | array         | Additional product images.                                                |
| data.getVouchers.data\[].parentProductId                | number / null | Parent product reference.                                                 |
| data.getVouchers.data\[].isDummyProduct                 | number        | Indicates if item is dummy/test (`0` or `1`).                             |
| data.getVouchers.data\[].redemptionFee                  | number        | Redemption fee amount.                                                    |
| data.getVouchers.data\[].redemptionFeeType              | string        | `percentage` or `fixed`.                                                  |
| data.getVouchers.data\[].redemptionFeeBorneByUser       | boolean       | Whether user pays the redemption fee.                                     |
| data.getVouchers.data\[].redemptionFeeTax               | number        | Tax on redemption fee.                                                    |
| data.getVouchers.data\[].is_free                        | number        | Whether voucher is free (`0` = paid, `1` = free).                         |

## Implementation Notes

1. To fetch exchangeRate in the GetVouchersAPI, pass "exchangeRate": 1 in the request body
2. To fetch the list of filters, use GetFiltersAPI
3. To fetch lounge in the GetVouchersAPI, pass "categoryType": "lounge" in the request body
4. If the value type for a product is **"open_value"**, please refer to the **"minValue"** and the **"maxValue"** parameters
5. The values passed in the **"fee"** and **"discount"** parameters are in percentage (%)
6. We recommend you cache the response from GetVouchersAPI in your database every time you sync our catalog
7. Use filters “minPrice” and “maxPrice” along with “currencyCode”, as this allows you to search prices with respect to a specific currency. If "currencyCode" code is not added, the filter will be applicable for all currencies.

> Learn about [Error Handling](https://developers.xoxoday.com/v1.2/docs/error-handling-1), [Rate limiting](https://developers.xoxoday.com/v1.2/docs/rate-limiting) and [Best Practice](https://developers.xoxoday.com/v1.2/docs/concepts-1) .
