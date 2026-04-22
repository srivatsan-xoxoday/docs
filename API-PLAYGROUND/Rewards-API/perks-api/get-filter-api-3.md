---
title: "Fetch Filter API"
slug: "get-filter-api-3"
excerpt: "Filters API allows you to identify filters that are available which can be applied to filter the products in Fetch Offers API"
hidden: false
createdAt: "Mon Aug 25 2025 05:02:22 GMT+0000 (Coordinated Universal Time)"
updatedAt: "Tue Dec 23 2025 13:47:15 GMT+0000 (Coordinated Universal Time)"
openapi: "API-PLAYGROUND/Rewards-API/perks-api/spec.yaml POST /fetchFilters"
---
## Request Schema

| Field            | Type       | Description                                                                           |
| ---------------- | ---------- | ------------------------------------------------------------------------------------- |
| `categoryType`   | String     | Defines the product category for which filters are requested.                         |
| `includeFilters` | String     | Comma-separated list of filter keys that must be explicitly included in the response. |
| `excludeFilters` | String     | Comma-separated list of filter keys that should be excluded from the response.        |
| `countryIds`     | Array  | List of country IDs used to scope filters based on regional availability.             |

## Response Schema

| Field Path                                         | Type   | Description                                                             |
| -------------------------------------------------- | ------ | ----------------------------------------------------------------------- |
| `data.fetchFilters.data.filters`                   | Array  | List of filter values applicable for the requested category and country |
| `data.fetchFilters.data.filters[].filter_value_id` | Number | Unique identifier of the filter value                                   |
| `data.fetchFilters.data.filters[].filter_value`    | String | Display name of the filter value                                        |
| `data.fetchFilters.data.filters[].image`           | String | Image URL associated with the filter value. Empty if not available      |
| `data.fetchFilters.data.filters[].filters`         | Array  | Nested filters under the filter value. Currently empty                  |
| `data.fetchFilters.data.filters[].categoryType`    | String | Category for which the filter applies (e.g. `offers`)                   |
| `data.fetchFilters.data.filters[].count`           | Number | Number of items available for this filter value                         |
| `data.fetchFilters.data.options`                   | Array  | Currently returned as an empty array for offers category                |
| `data.fetchFilters.data.brands`                    | Array  | Currently returned as an empty array for offers category                |
| `data.fetchFilters.data.countries`                 | Array  | Country-wise aggregation of available items                             |
| `data.fetchFilters.data.countries[].countryId`     | Number | Internal country identifier                                             |
| `data.fetchFilters.data.countries[].countryName`   | String | Name of the country                                                     |
| `data.fetchFilters.data.countries[].count`         | String | Total number of items available for the country                         |
