# HTTP status codes

## 200 OK

The request has been accepted and processed. The response contains a [JSON object](../output/index.md).

## 401 Unauthorized

The reasons for this state can be:

- the [authorization token](../../how-to/#authentication-and-authorization) is missing
- the authorization token is not valid
- the authorization token has expired
- the [execution key](../../how-to/#execution-key) is missing
- the execution key is not valid

## 403 Forbidden

This code is returned when one or more of the plan limits&mdash;for example the calls per month limit&mdash;have been reached.

## 404 Not Found

The server can not find the requested resource, the URL is wrong.
    
## 500 Internal Server Error

The server has encountered a situation it doesn't know how to handle.  
It can happen when the JSON object _posted_ with the request is invalid.

For example, the following is not a valid JSON object because both the external curly braces and the quotation marks around the properties names are missing.

    document: {
        text: "Michael Jordan was one of the best basketball players of all time. Scoring was Jordan's stand-out skill, but he still holds a defensive NBA record, with eight steals in a half."
    }