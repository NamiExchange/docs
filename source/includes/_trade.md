# Trading

## Get Opening Order

```shell
curl "https://nami.exchange/api/v1.0/spot/order"
```
> The above command returns JSON structured like this:

```json
{
	"status": "ok",
	"data": [
	{
		"id": null,
		"user_id": 18,
		"action": "BUY",
		"type": "STOP_LIMIT",
		"status": "PENDING",
		"quantity": 1,
		"price": 1,
		"stopPrice": 0.5,
		"base_currency": "USDT",
		"exchange_currency": "NAC",
		"created_at": "2019-12-26T11:29:23.721Z"
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


### Response Content
Field	|   Data Type	|   Description
---     |   ---         |    ---
id                  |Integer| Order ID
symbol              |String| Order Symbol
status              |String| Order Side (BUY, SELL)
side                |String| Order Side (BUY, SELL)
type                |String| Order Type  (MARKET, LIMIT, STOP_LIMIT)
quantity            |String| Order Amount
price               |String| Order Price
stop_price          |String| Order Stop Price for STOP_LIMIT
created_at          |Date| The timestamp when the order was created

## Get History Order

```shell
curl "https://nami.exchange/api/v1.0/spot/order_history"
```

> The above command returns JSON structured like this:

```json
{
	"status": "ok",
	"data": [
	{
        "id": 21,
        "symbol": "NACUSDT",
        "action": "BUY",
        "type": "LIMIT",
        "status": "SUCCESS",
        "quantity": 10000,
        "price": 1,
        "created_at": "2019-12-27T03:03:56.497Z"
    }]
}
```
API Key Permission：Read
This endpoint submit a request to create an order.
### HTTP Request
      
`POST https://nami.exchange/api/v1.0/spot/order_history`
### Query Parameters
Parameter	|Data Type	|Required	|Default Value	|Description	|Value Range
    ---     |       --- |       --- |           --- |           --- |---
page	|Integer	|false	|0	|Page index	| 0, 1, 2,...
page_size	|Integer	|false	|20	|Size of page	| Max: 100

### Response Content
Field	|   Data Type	|   Description
---     |   ---         |    ---
id                  |Integer| Order ID
symbol              |String| Order Symbol
status              |String| History Status (MATCH_ORDER, CLOSE_ORDER)
side                |String| Order Side (BUY, SELL)
type                |String| Order Type  (MARKET, LIMIT, STOP_LIMIT)
quantity            |String| Order Amount
price               |String| Order Price
stop_price          |String| Order Stop Price for STOP_LIMIT
created_at          |Date| The timestamp when the order was created

## Place a New Order

```shell
curl -X POST -H "Content-Type: application/json" "https://nami.exchange/api/v1.0/spot/order" -d
'{
    "symbol": "NACUSDT",
    "side": "SELL",
    "type": "MARKET",
    "quantity": 1000,
    "price": 1,
    "stop_price": 0
}'
```

> The above command returns JSON structured like this:

```json
{  
   "status":"ok",
   "data":{  
      "symbol":"NACUSDT",
      "side":"SELL",
      "type":"MARKET",
      "exchange_amount":1,
      "avg_price":1
   }
}
```
API Key Permission：Exchange
This endpoint submit a request to create an order.
### HTTP Request
      
`POST https://nami.exchange/api/v1.0/spot/order`
### Body Parameters
Parameter	|Data Type	|Required	|Default Value	|Description	|Value Range
    ---     |       --- |       --- |           --- |           --- |---
symbol	|string	|true	|NA	|The trading symbol to query	|All supported trading symbols, e.g. btcusdt, ethusdt
side	|string	|true	|NA	|The trading side	|BUY, SELL
type	|string	|true	|NA	|The trading type	|MARKET, LIMIT, STOP_LIMIT
quantity	|double	|true	|NA	|The trading quantity	|
price	|string	|true	|NA	|	|Limit price of limit or stop-limit order
stop_price	|string	|true	|NA	|	|Stop price of stop-limit order


### Response Content
Field	|   Data Type	|   Description
---     |   ---         |    ---
id                  |Integer| Order ID
symbol              |String| Order Symbol
side                |String| Order Side (BUY, SELL)
type                |String| Order Type  (MARKET, LIMIT, STOP_LIMIT)
quantity            |String| Order Amount
price               |String| Order Price
stop_price          |String| Order Stop Price for STOP_LIMIT
avg_price           |String| Order Avg Price for MARKET

## Delete Order

```shell
curl --location --request DELETE 'https://nami.exchange/api/v1.0/spot/order' \
--header 'Content-Type: application/json' \
--data-raw '{
	"id": 1238912
}'
```

> The above command returns JSON structured like this:

```json
{  
   "status":"ok",
   "data":{  
      "id":1238912
   }
}
```
API Key Permission：Exchange
This endpoint submit a request to create an order.
### HTTP Request
      
`POST https://nami.exchange/api/v1.0/spot/order`
### Body Parameters
Parameter	|Data Type	|Required	|Default Value	|Description	|Value Range
    ---     |       --- |       --- |           --- |           --- |---
id	|Integer	|true	|NA	|Order ID	|


### Response Content
Field	|   Data Type	|   Description
---     |   ---         |    ---
id                  |Integer| Order ID

