---
title: "Get Campaign Details API"
slug: "get-campaign-details-api"
excerpt: "The Get Campaign Details API can be used to fetch the products included in a specific Campaign."
hidden: false
createdAt: "Fri Apr 07 2023 06:38:45 GMT+0000 (Coordinated Universal Time)"
updatedAt: "Mon Nov 24 2025 06:00:11 GMT+0000 (Coordinated Universal Time)"
openapi: "reward-link-spec.yaml POST /campaignDetails"
---
## Get Campaign Details Schema

| **Property** | **Type** | **Description**                             |
| :----------- | :------- | :------------------------------------------ |
| `campaignId` | `Int`    | Unique identifier of the campaign to fetch. |

## Response Schema

| **Property**                                    | **Type** | **Description**                                          |
| ----------------------------------------------- | -------- | -------------------------------------------------------- |
| data                                            | object   | Root response object.                                    |
| data.campaignDetails                            | object   | Container for campaign details.                          |
| data.campaignDetails.success                    | number   | API execution status (`1` = success).                    |
| data.campaignDetails.data                       | array    | List containing campaign detail entries.                 |
| data.campaignDetails.data\[].campaignId         | number   | Unique campaign ID.                                      |
| data.campaignDetails.data\[].campaignName       | string   | Name of the campaign.                                    |
| data.campaignDetails.data\[].denomination_value | number   | Denomination/value associated with the campaign.         |
| data.campaignDetails.data\[].currency_code      | string   | Currency code for denomination.                          |
| data.campaignDetails.data\[].countryName        | string   | Applicable country for the campaign.                     |
| data.campaignDetails.data\[].vouchers           | array    | List of vouchers/products associated with this campaign. |
| data.campaignDetails.data\[].vouchers\[].name   | string   | Voucher/product name.                                    |
| data.campaignDetails.data\[].vouchers\[].image  | string   | Image URL for the voucher/product.                       |
