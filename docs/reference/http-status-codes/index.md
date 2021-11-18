# HTTP status codes

Status codes are part of the HTTP/HTTPS protocol and are issued by essex in response to a client's request.

## 200 OK

The request has been accepted and processed. The response contains a [JSON object](../output/index.md).

## 400 Bad Request

The server cannot or will not process the request due to something that is perceived to be a client error (e.g., malformed request syntax).  
It can happen when the JSON object _posted_ with the [request](../requests/index.md) is invalid.

## 404 Not Found

The server can not find the requested resource, the URL is wrong.
    
## 500 Internal Server Error

The server has encountered a situation it doesn't know how to handle.  