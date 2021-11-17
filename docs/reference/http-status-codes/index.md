# HTTP status codes

Status codes are part of the HTTP/HTTPS protocol and are issued by essex in response to a client's request.

## 200 OK

The request has been accepted and processed. The response contains a [JSON object](../output/index.md).

## 404 Not Found

The server can not find the requested resource, the URL is wrong.
    
## 500 Internal Server Error

The server has encountered a situation it doesn't know how to handle.  
It can happen when the JSON object _posted_ with the request is invalid.