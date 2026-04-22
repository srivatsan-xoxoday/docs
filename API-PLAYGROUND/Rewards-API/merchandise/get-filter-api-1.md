---
title: "Get Filter API"
slug: "get-filter-api-1"
excerpt: "Filters API allows you to identify filters that are available which can be applied to filter the products in Get Merchandise API"
hidden: false
createdAt: "Thu Aug 21 2025 10:24:54 GMT+0000 (Coordinated Universal Time)"
updatedAt: "Sat Nov 22 2025 21:00:49 GMT+0000 (Coordinated Universal Time)"
openapi: "API-PLAYGROUND/Rewards-API/merchandise/spec.yaml POST /getFilters"
---
## Note:

1. In the getFilter API Request, "includeFilters" & " excludeFilters " will only work by passing value in " filterGroupCode "
2. You can pass empty values in the getFilters API request for all the parameters to get a list of all the available filters

## Request Schema

| **Property**      | **Type** | **Description**                                                    |
| :---------------- | :------- | :----------------------------------------------------------------- |
| `filterGroupCode` | `string` | filter category name  representing a specific filter group applied |
| `includeFilters`  | `string` | Filters that should be explicitly included                         |
| `excludeFilters`  | `string` | Filters that should be explicitly excluded                         |

## Response Schema

| **Path**                                               | **Type** | **Description**                                                     |
| ------------------------------------------------------ | -------- | ------------------------------------------------------------------- |
| **data**                                               | object   | Root object containing the `getFilters` payload.                    |
| **data.getFilters**                                    | object   | Main container for filter metadata.                                 |
| **data.getFilters.status**                             | number   | API execution status. `1` indicates success.                        |
| **data.getFilters.data**                               | array    | List of filter groups supported by the catalog.                     |
| **data.getFilters.data\[].filterGroupName**            | string   | Display name of the filter group (e.g., Country).                   |
| **data.getFilters.data\[].filterGroupDescription**     | string   | Description of the filter group.                                    |
| **data.getFilters.data\[].filterGroupCode**            | string   | Internal code for the filter group (e.g., `country`).               |
| **data.getFilters.data\[].filters**                    | array    | List of filter values inside the group.                             |
| **data.getFilters.data\[].filters\[].filterValue**     | string   | Display name of the filter value (e.g., Afghanistan).               |
| **data.getFilters.data\[].filters\[].isoCode**         | string   | Short ISO code for the filter (e.g., AF).                           |
| **data.getFilters.data\[].filters\[].filterValueCode** | string   | Internal system code used in downstream APIs (e.g., `afghanistan`). |

## List of available filterGroupCode

| **Filter name**  | **Functionality**                                                                          |
| :--------------- | :----------------------------------------------------------------------------------------- |
| country          | Users can filter products based on the country                                             |
| price            | Users can filter products based on price range (0 – 1,000, 10,000 – above, etc.)           |
| voucher_category | Users can filter products based on categories like Electronics, Food & Restaurant          |
| product_category | Users can filter products based on types like e-gift voucher, Experience, Physical voucher |
| currency         | Users can filter products based on the product currency (INR, USD, AUD, etc.)              |
| merchandise      | Users can filter products based on merchandise categories (e.g., Apparel, Home, Lifestyle) |
