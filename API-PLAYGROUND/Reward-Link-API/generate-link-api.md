---
title: "Generate Link API"
slug: "generate-link-api"
excerpt: "The Generate Link API allows you to generate links in bulk for reward distribution. The API is useful for reward automation without the recipient's email address."
hidden: false
createdAt: "Fri Apr 07 2023 06:46:06 GMT+0000 (Coordinated Universal Time)"
updatedAt: "Mon Nov 24 2025 06:01:15 GMT+0000 (Coordinated Universal Time)"
openapi: "reward-link-spec.yaml POST /generateLink"
mode: "default"
---

## Generate Link API Schema

| **Property** | **Type** | **Description** |
| :-- | :-- | :-- |
| `campaignId` | `String` | Unique identifier of the campaign for which the link(s) should be generated. |
| `links_quantity` | `Int` | Number of links to generate. |
| `link_expiry` | `String` | Expiry date for the link(s) (format: `DD-MM-YYYY`). |

## Response Schema

| **Path** | **Type** | **Description** |
| --- | --- | --- |
| data | object | Root response object. |
| data.generateLink | object | Container for link generation result. |
| data.generateLink.success | number | API execution status (`1` = success). |
| data.generateLink.message | string | Message returned by the API. |
| data.generateLink.links | array | List of generated reward/claim links. |
| data.generateLink.links\[\] | string | Individual generated link URL. |
| data.generateLink.batchId | string | Unique batch identifier for the generated link set. |
| data.generateLink.campaignName | string | Name of the campaign for which links were generated. |
| data.generateLink.campaignId | string | Campaign ID (string returned by API). |
| data.generateLink.denomination\_value | number | Denomination/value associated with the generated links. |
| data.generateLink.countryName | string | Country for which the link campaign applies. |
| data.generateLink.currencyCode | string | Currency code for the denomination. |