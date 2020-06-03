# Errors

The Scout API returns predictable error responses.
You'll receive a `message` parameter that describes the error, and one of the following status codes:

```json
{
  "success": false,
  "message": "Descriptive message of what went wrong"
}
```

> A JSON response in this format will be returned if you run into an error


Error Code | Meaning
---------- | -------
400 | Your request is invalid.
403 | Incorrect API key or incorrect access_token.
404 | Not Found.
422 | Could not process request.
500 | We had a problem with our server. Try again.
503 | We're temporarily offline for maintenance. Please try again later.
