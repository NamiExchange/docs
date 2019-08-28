# API Access
## Access URLs
* The base endpoint is: `https://nami.exchange/api/v1.0`
* All REST requests must be sent using the application/json content type. Non-HTTPS requests will be redirected to HTTPS, possibly causing functional or performance issues with your application.
* All REST requests will result in a `200 Ok` response unless there is a server or infrastructure error. The API result will be wrapped in a JSON Result object, where the `status` field indicates response status.

## Endpoint Rate Limit
The Nami.Exchange API employs call limits on all endpoints to ensure the efficiency and availability of the platform for all customers. In general, API users are permitted to make a maximum of 60 API calls per minute. Calls after the limit will fail, with the limit resetting at the start of the next minute. If your IP reachs rate limit too much, your IP will be banned within 1 hour. So, always pay attention to the frequency of requests
## Request Format
All API requests are in either GET or POST method. For GET request, all parameters are path parameters. For POST request, all parameters are in POST body and in JSON format.
## Response Format
All response will be returned in JSON format. The top level JSON is a wrapper object which has metadata "status". The actual per API response data is in "data" field.
**Response JSON Wrapper Content**

> Response wrapper content example:

```json
{
  "status": "ok",
  "data":  "API response data in nested JSON object"
}
```
Field	|Data Type	|Description
---	|---	|---
status	|string	|The overall API call result status
data	|object	|The actual response content per API
