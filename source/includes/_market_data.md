# Market Data

## Get Exchange Info

```shell
curl "https://nami.exchange/api/v1.0/market/symbols"
```


> The above command returns JSON structured like this:

```json
{
    "status": "ok",
    "data": [
        {
            "symbol": "ETHUSDT",
            "exchange_currency": "ETH",
            "base_currency": "USDT",
            "status": "TRADING",
            "min_price": 0.0001,
            "max_price": 1000000,
            "tick_size": 0.01,
            "step_size": 0.00001,
            "min_qty": 0.00001,
            "max_qty": 9000,
            "min_notional": 10
        }
    ]
}
```

Current exchange trading rules and symbol information

### HTTP Request

`GET /market/symbols`

### Response Content
Field	|   Data Type	|   Description
---     |   ---         |    ---
symbol  | string | The trading symbol of this object, e.g. btcusdt, bccbtc
base_currency   | string | Base currency, for example: with symbol BTCUSDT, base currency is USDT
exchange_currency   | string | Exchange currency, for example: with symbol BTCUSDT, base currency is BTC
min_price | float | Min exchange rate
max_price | float | Max exchange rate
tick_size | float | Min exchange rate movement
step_size | float | Min exchange amount movement
min_qty | float | Min exchange amount
max_qty | float | Max exchange amount
min_notional | float | Min value of exchange_rate*exchange_amount
## Get 24hr ticker price

```shell
curl "https://nami.exchange/api/v1.0/market/summaries"
```


> The above command returns JSON structured like this:

```json
{
    "status": "ok",
    "data": [
         {
            "symbol": "BTCUSDT",
            "last_price": 10090.8,
            "change_24h": 10,
            "last_price_24h": 10080.8,
            "high_24h": 10099.8,
            "low_24h": 10079.8,
            "high_1h": 10099.8,
            "low_1h": 10079.8,
            "total_exchange_volume": 20.459,
            "total_base_volume": 206232.93,
            "base_currency": "USDT",
            "exchange_currency": "BTC"
        }
    ]
}
```

Get 24h ticker data of all available symbols or specific symbol.

### HTTP Request

`GET /market/summaries`

### Query Parameters
Parameter	|Data Type	|Required	|Default Value	|Description	|Value Range
    ---     |       --- |       --- |           --- |           --- |---
symbol	|string	|false	|NA	|The trading symbol to query	|All supported trading symbols, e.g. btcusdt, ethusdt

### Response Content
Field	|   Data Type	|   Description
---     |   ---         |    ---
symbol  | string | The trading symbol of this object, e.g. btcusdt, bccbtc
last_price  | float | The last price
change_24h  | float | Change compare to last  24 hours price
last_price_24h  | float | Last price 24 hours
high_24h    | float|The high price of last 24 hours
low_24h | float|The low price of last 24 hours
high_1h | float|The high price of last 1 hours
low_1h  | float   |The low price of last 1 hours
total_exchange_volume   | float| The trading volume in exchange currency of last 24 hours
total_base_volume   | float| The trading volume in base currency of last 24 hours
base_currency   | string | Base currency, for example: with symbol BTCUSDT, base currency is USDT
exchange_currency   | string | Exchange currency, for example: with symbol BTCUSDT, base currency is BTC

## Get Market Depth

```shell
curl "https://nami.exchange/api/v1.0/market/depth?symbol=ETHUSDT"
```


> The above command returns JSON structured like this:


```json
{
    "status": "ok",
    "data": {
        "bids": [
            {
                "amount": 0.521268,
                "exchange_rate": 186.01,
                "action": "BUY"
            }
        ],
        "asks": [
            {
                "amount": 0.9578,
                "exchange_rate": 192.99,
                "action": "SELL"
            }
        ]
    }
}
```

This endpoint retrieves the current order book of a specific symbol.

### HTTP Request

`GET /market/depth`

### Query Parameters
Parameter	|Data Type	|Required	|Default Value	|Description	|Value Range
    ---     |       --- |       --- |           --- |           --- |---
symbol	|string	|true	|NA	|The trading symbol to query	|All supported trading symbols, e.g. btcusdt, ethusdt
limit	|int	|false	|20	|Limit depth of order book	|[1-20]

### Response Content
Field	|   Data Type	|   Description
---     |   ---         |    ---
bids  | object | The current all bids in format [amount, exchange_rate, action]
asks  | ojbject | The current all asks in format [amount, exchange_rate, action]

## Get the Most Recent Trades

```shell
curl "https://nami.exchange/api/v1.0/market/history/trade?symbol=ETHUSDT"
```


> The above command returns JSON structured like this:


```json
{
    "status": "ok",
    "data": [
        {
            "direction": "SELL",
            "exchange_rate": 0.00652,
            "exchange_amount": 3354,
            "base_amount": 21.86808,
            "created_at": 1567006044486
        }
    ]
}
```

This endpoint retrieves the most recent trades with their exchange rate, base amount, exchange amount, and direction.

### HTTP Request

`GET /market/history/trade`

### Query Parameters
Parameter	|Data Type	|Required	|Default Value	|Description	|Value Range
    ---     |       --- |       --- |           --- |           --- |---
symbol	|string	|true	|NA	|The trading symbol to query	|All supported trading symbols, e.g. btcusdt, ethusdt
limit	|int	|false	|20	|Limit depth of order book	|[1-100]

### Response Content
<aside class="notice">
The returned data object is an array represents all trades occurred.
</aside>
Field	|   Data Type	|   Description
---     |   ---         |    ---
base_amount|	float|	The trading volume in base currency
exchange_amount|	float|	The trading volume in exchange currency
exchange_rate|	float|	The trading price in quote currency
created_at|	integer|	The UNIX timestamp in milliseconds
direction|	string|	The direction of the taker trade: 'BUY' or 'SELL'



## Get Tickers Data

```shell
curl "https://data.nami.exchange/nami/prices/history?symbol=BTCUSDT&resolution=60&from=1606017873&to=1606104273"
```


> The above command returns JSON structured like this:


```json
{
    "t": [1606093200, 1606096800, 1606100400, 1606104000],
    "o": [741, 779, 765, 760],
    "h": [782, 779, 774, 763],
    "l": [736, 760, 760, 757],
    "c": [779, 765, 760, 759],
    "v": [0, 0, 0, 0],
    "s": "ok"
}
```

This endpoint retrieves the ticker data with open, close, high, low and time of ticker.

### HTTP Request

`GET https://data.nami.exchange/nami/prices/history`

### Query Parameters
Parameter	|Data Type	|Required	|Default Value	|Description	|Value Range
    ---     |       --- |       --- |           --- |           --- |---
symbol	|string	|true	|NA	|The trading symbol to query	|All supported trading symbols, e.g. btcusdt, ethusdt
resolution	|string	|true	|20	|Timeframe of ticker	|[1, 60, D]
from	|int	|true	|20	|From in timestamp	|[1-100]
to	|int	|true	|20	|To in timestamp	|[1-100]

### Response Content
<aside class="notice">
The returned data object is an array represents all trades occurred.
</aside>
Field	|   Data Type	|   Description
---     |   ---         |    ---
t|	float|	Time of tickers in array
o|	float|	Open Data of tickers in array
h|	float|	High Data of tickers in array
l|	integer|	Low Data of tickers in array
v|	string|	Volume of tickers in array
s|	string|	Status
