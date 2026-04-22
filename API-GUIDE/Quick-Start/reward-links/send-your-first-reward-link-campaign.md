---
title: "Send Your First Reward Link"
slug: "send-your-first-reward-link-campaign"
excerpt: "This section will guide you on how you can send your first reward link via API"
hidden: false
createdAt: "Mon Aug 18 2025 08:51:04 GMT+0000 (Coordinated Universal Time)"
updatedAt: "Fri Oct 24 2025 07:27:41 GMT+0000 (Coordinated Universal Time)"
---
Once you’ve created a campaign in the Plum Admin Dashboard, follow the steps below to send a Reward Link using APIs:

1. **Get Campaign ID**  
   First, fetch the list of campaigns from your Plum dashboard to get the campaignId of the campaign you want to use.

### Request

```json
curl --location 'https://stagingstores.xoxoday.com/chef/v1/oauth/api' \
--header 'Authorization: Bearer <your-access-token>' \
--header 'content-type: application/json' \
--header 'Authorization: ••••••' \
--data '{
  "tag":"xoxo_link",
  "query":"xoxo_link.query.campaignList",
  "variables" : { "add_data": { "limit": 10, "offset": 0, "name": "", "enabled" : 1} }

}'
```

### Response

```json
{
    "data": {
        "campaignList": {
            "success": 1,
            "data": [
                {
                    "campaignId": 2461,
                    "campaignName": "Test Campaign",
                    "denomination_value": 10,
                    "countryName": "USA",
                    "currencyCode": "USD",
                    "created_date": "0000-00-00 00:00:00",
                    "product_count": "1",
                    "status": 1
                }
            ],
            "count": 1,
            "errors": null
        }
    }
}
```

<br />

2. **Send Reward Link**  
   Now use the retrieved campaignId to send a Reward Link to a recipient.

### Request

```json
curl --location 'https://canvas.xoxoday.com/chef/v1/oauth/api/sendLinks' \
--header 'Authorization: Bearer <your-access-token>' \
--header 'content-type: application/json' \
--header 'Authorization: ••••••' \
--data-raw '{
    "query": "xoxo_link.mutation.generateLinkEmail",
    "tag": "xoxo_link",
    "variables": {
        "data": {
            "campaignId": "2455",
            "email_ids": "youeemail@example.com",
            "link_expiry": "31-07-2026"
        }
    }
}'
```

### Response

```json
{
    "data": {
        "generateLink": {
            "success": 1,
            "message": "Links created successfully"
        }
    }
}
```

<br />

3. **Reward Link Delivery**  
   Once the request is successful, the recipient will receive an email with their Reward Link.

```mermaid
graph TD
  A[block:image] --> B{
  "images": [
    {
      "image": [
        "https://files.readme.io/8e340cb67b03695215cc6788666a6293b9c3cb3c87c5d59974f0988e4eff5e5e-image.png",
        null,
        ""
      ],
      "align": "center",
      "sizing": "60% "
    }
  ]
}
  B --> C[/block]
```

<br />

That’s it! You’ve successfully created and sent a Reward Link via the Reward Link APIs.