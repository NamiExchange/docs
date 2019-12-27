# Authentication

## Public API
The Market Data API (`https://nami.exchange/api/v1.0/market`) does not require authentication.


    'api-expires': expires,
    'api-key': apiKey,
    'api-signature': signature,
    
    
## Authentication using API key
Authentication is done by sending the following HTTP headers:

- api-expires: A UNIX timestamp in seconds after which the request is no longer valid. This is to prevent replay attacks.
- api-key: Your public API key.
- api-signature: A signature of the request you are making. It is calculated as hex(HMAC_SHA256(apiSecret, verb + path + expires + data)). See the example calculations below.

## Example using API key
Use these calculations as test cases in your code.
```shell
apiKey = 'zukHJtjyIKUN22WhrkNSzf54CzsMtR4m'
apiSecret = 'bXKoe2Gr3nes99nMmpu44h7hCNQlZf6GAPJ3oAueRcRYWpdnhWKgVu64roeOO7Gh'

#
# Simple GET 
# Get user wallet from /api/v1.0/user/wallet
#
verb = 'GET'
url = /api/v1.0/user/wallet
params = {
    currency: 'ETH'
}
=> path = '/api/v1.0/user/wallet?currency=ETH'
expires = 1518064236 # Friday, December 27, 2019 4:39:51 AM
data = ''

# signagure = HEX(HMAC_SHA256(apiSecret, verb + path + str(expires) + data))
# signagure = HEX(HMAC_SHA256(apiSecret, 'GET/api/v1.0/user/wallet?currency=ETH1577421591'))
# signagure = 'e24d08880b9d9b6c1f77fecc5977ed1a9ee1102ab0f34757e792057f1c78a3a5'


#
# Simple POST 
# Create new Order from /api/v1.0/spot/order
#
verb = 'POST'
url = /api/v1.0/spot/order
params = {}
=> path = '/api/v1.0/spot/order'
expires = 1577421880 # Friday, December 27, 2019 4:44:40 AM
data = { 
    symbol: 'NACUSDT',
    side: 'BUY',
    type: 'LIMIT',
    quantity: 1,
    price: 1,
    stop_price: 0 
}

# signagure = HEX(HMAC_SHA256(apiSecret, verb + path + str(expires) + data))
# signagure = HEX(HMAC_SHA256(apiSecret, 'POST/api/v1.0/spot/order1577421880{"symbol":"NACUSDT","side":"BUY","type":"LIMIT","quantity":1,"price":1,"stop_price":0}'))
# signagure = '986ac8fa1d263cd047aa7791be3f185fe892ce4dbfc9c8d09fc3a2f39715cddb'

```

## Troubleshooting

**If you are receiving "Invalid API Key" messages, check the following:**

-  Doube check your API public key is exact.

**If you are receiving "Invalid API Permission" messages, check the following:**

-  Your API key permisson is valid. The permission require is described in api docs.
 
**If you are receiving "Signature Not Valid" messages, check the following:**

- Check that your signatures match the sample signatures above.
- If there is a request body, make sure your Content-Length and Content-Type are valid.
- Ensure your request body is being properly sent. Try a few sample requests against httpbin.
- Ensure you are signing the exact string that is being sent to the server. Certain JSON serializers have unstable key ordering, so serialize to a string first, sign that string, and then send the same string in the request body.
