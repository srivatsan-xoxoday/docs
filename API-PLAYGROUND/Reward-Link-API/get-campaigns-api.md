---
title: "Get Campaigns API"
slug: "get-campaigns-api"
excerpt: "The Get Campaigns API is useful to get the list of all the campaigns created from the dashboard."
hidden: false
createdAt: "Fri Apr 07 2023 06:13:37 GMT+0000 (Coordinated Universal Time)"
updatedAt: "Mon Nov 24 2025 05:59:18 GMT+0000 (Coordinated Universal Time)"
openapi: "reward-link-spec.yaml POST /campaignList"  
---
## Get Campaigns API Schema

| **Property** | **Type** | **Description**                                                    |
| :----------- | :------- | :----------------------------------------------------------------- |
| `limit`      | `Int`    | Number of campaigns to fetch (pagination limit).                   |
| `offset`     | `Int`    | Starting index for fetching campaigns (pagination offset).         |
| `name`       | `String` | Filter campaigns by name (optional, empty string means no filter). |
| `enabled`    | `Int`    | Filter by campaign status (1 = enabled, 0 = disabled).             |

## Response Schema

| **Path**                                     | **Type** | **Description**                                              |
| -------------------------------------------- | -------- | ------------------------------------------------------------ |
| data                                         | object   | Root response object.                                        |
| data.campaignList                            | object   | Container for campaign list.                                 |
| data.campaignList.success                    | number   | API execution status (`1` = success).                        |
| data.campaignList.data                       | array    | List of campaigns.                                           |
| data.campaignList.data\[].campaignId         | number   | Unique campaign identifier.                                  |
| data.campaignList.data\[].campaignName       | string   | Name of the campaign.                                        |
| data.campaignList.data\[].denomination_value | number   | Campaign denomination or value associated with the campaign. |
| data.campaignList.data\[].countryName        | string   | Country where campaign is applicable.                        |
| data.campaignList.data\[].currencyCode       | string   | Currency code for denomination.                              |
| data.campaignList.data\[].created_date       | string   | Creation timestamp of the campaign.                          |
| data.campaignList.data\[].product_count      | number   | Number of products linked to this campaign.                  |
| data.campaignList.data\[].status             | number   | Status (`1` = active, `0` = inactive).                       |
