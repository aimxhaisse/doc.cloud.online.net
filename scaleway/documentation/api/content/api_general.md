FORMAT: 1A

# Welcome to the Scaleway API documentation. This API provides access to Scaleway services.

## Request and response

The scaleway api works over https and is accessed from the `api.scaleway.com` domain. All data is sent and received as json. All data is sent and received as json.

## Constructing Requests

Requests are made of two components:

- API version
- Resource path

To construct a proper request, you will need to format the URI as follows:

`https://api.scaleway.com/{version}/{ressource}`

An example request, to retrieves detailed informations about an instance might be:

```
curl -i 'https://api.scaleway.com/v1/organizations' --header "X-Auth-Token: fa6316e3-3c71-4304-8a08-f9d07207e240"

HTTP/1.0 200 OK
Content-Type: application/json
Content-Length: 213
Access-Control-Allow-Origin: *
Access-Control-Expose-Headers: content-type, x-auth-token, location
Access-Control-Allow-Headers: content-type, x-auth-token, location
Access-Control-Allow-Methods: POST, PUT, DELETE, GET, OPTIONS, PATCH, HEAD
Access-Control-Allow-Credentials: true
Server: nginx
Date: Mon, 03 Feb 2014 16:55:04 GMT

{
  "organizations": [
    {
      "id": "22222222-1111-4111-8111-222222222222",
      "name": "General Inc"
    },
    {
      "id": "11111111-1111-4111-8111-111111111111",
      "name": "Scaleway"
    }
  ]
}
```

## Error

Scaleway uses conventional HTTP response codes to indicate success or failure of an API request. In general, codes in the 2xx range indicate success, codes in the 4xx range indicate an error that resulted from the provided information (e.g. a required parameter was missing, a charge failed, etc.), and codes in the 5xx range indicate an error with Scaleway's servers.

### HTTP Status Code Summary

- 200 OK - Everything worked as expected.
- 400 Bad Request - Often missing a required parameter.
- 401 Unauthorized - No valid API key provided.
- 402 Request Failed - Parameters were valid but request failed.
- 404 Not Found - The requested item doesn't exist.
- 500, 502, 503, 504 Server errors - something went wrong on Scaleway's end.

Not all errors map cleanly onto HTTP response codes, however. When a request is valid but does not complete successfully (e.g. an instance can not be launch), we return a 402 error code.

### Attributes

- type:
 - invalid_request_error: Occured when your request has an invalid parameters
 - api_error: API errors is used in case of problem with Scaleway's servers
- message:
 - A human readable error giving more details about the error
- code (Optional):
 - For ressources errors, it's a short string describing error that occurred.
- param (Optional):
 - The parameter the error relates to if the error is parameter-specific.

### Pagination

Methods returning multiple items are paginated to 25 items by default.
You can specify further pages with the ?page parameter. You can also set a custom page size up to 500 with the ?page_size parameter.

```
$curl -i https://api.scaleway.com/v1/servers/Server-198779b8-e4b5-4876-9e2f-aa09c1ce9ebf/tags?page=5&page_size=150

HTTP/1.1 200 OK
Content-Type: application/json; charset=utf-8
Status: 200 OK
X-RateLimit-Limit: 5000
X-RateLimit-Remaining: 4999
X-RateLimit-Reset: 1389359739
Link: <https://api.scaleway.com/v1/servers/Server-198779b8-e4b5-4876-9e2f-aa09c1ce9ebf/tags?page=1&page_size=150>; rel="first", <https://api.scaleway.com/v1/servers/Server-198779b8-e4b5-4876-9e2f-aa09c1ce9ebf/tags?page=4&limit=150>; rel="prev", <https://api.scaleway.com/v1/servers/Server-198779b8-e4b5-4876-9e2f-aa09c1ce9ebf/tags?page=6&limit=150>; rel="next", <https://api.scaleway.com/v1/servers/Server-198779b8-e4b5-4876-9e2f-aa09c1ce9ebf/tags?page=10&limit=150>; rel="last",
...

{
  "tags": {
    ...
  }
}
```

## Resources
