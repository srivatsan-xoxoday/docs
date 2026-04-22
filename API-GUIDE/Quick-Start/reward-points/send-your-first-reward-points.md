Let’s send ourselves a test reward of 500 points to confirm everything is working.

Run the following cURL command, replacing:

1. YOUR-ACCESS-TOKEN with your generated API key
2. YOUR-EMAIL-ADDRESS with your email address in `sender_email`
3. RECIPIENT-EMAIL-ADDRESS with your email address in `to_email`

```json
curl --request POST \
     --url https://stagingstores.xoxoday.com/chef/v1/oauth/api \
     --header 'Authorization: Bearer <your-access-token>' \
     --header 'content-type: application/json' \
     --data '{
    "query": "storesAdmin.mutation.sendBalance",
    "tag": "storeAdmin",
    "variables": {
        "recipients_data": {
            "sender_email": "youremail@example.com",
            "recipients": [
                {
                    "to_name": "name1",
                    "to_email": "email1@xyz.com",
                    "amount": "500",
                    "citation": "Congratulations"
                }
            ]
        }
    }
}'
```

## Response

```json
{
  "data": {
    "sendBalance": {
      "error": false,
      "message": "points sent"
    }
  }
}
```

Congratulations — you’ve successfully made your first points transfer.