# User

## Get User Wallet

```shell
curl "https://nami.exchange/api/v1.0/user/wallet"
```

> The above command returns JSON structured like this:

```json
{
	"status": "ok",
	"data": [
	{
        "currency": "NAC",
        "value": 2465,
        "locked_value": 0
    },
    {
        "currency": "ETH",
        "value": 1009.8500524310101,
        "locked_value": 0.10001
    },
    {
        "currency": "DAI",
        "value": 10000,
        "locked_value": 0
    },
    {
        "currency": "SPIN",
        "value": 26058.942333333325,
        "locked_value": 11271
    }]
}
```
API Key Permission：Read
This endpoint submit a request to create an order.
### HTTP Request
      
`POST https://nami.exchange/api/v1.0/spot/order`
### Query Parameters
Parameter	|Data Type	|Required	|Default Value	|Description	|Value Range
    ---     |       --- |       --- |           --- |           --- |---
    currency	|String	|false	|NA	|Filter Currency	| Supported Currency
### Response Content
Field	|   Data Type	|   Description
---     |   ---         |    ---
currency              |String| Currency
value              |Double| Balance of user
locked_value              |Double| Lock value in spot, futures,...


