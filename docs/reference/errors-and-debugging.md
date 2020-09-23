# Errors & Debugging

A Decode error response looks like this:

```jsx
{
  "ok": false,
  "who": "upstream",
  "error": {
    "summary": "Query to database hit timeout limit (10s)"
  }
}
```

- `ok` - whether or not the request succeeded
- `who` - who is "responsible" for the error. Possible values are `you`, `decode`, and `upstream` (the API or database you are calling).
- `error.summary` - Decode tries its best to unpack and describe the error

Here are some of the error status codes you might receive:

`**422**`

This means the gateway was "unreachable." This is most commonly experienced when Decode can't connect to a database.

**`502`**

This means the _upstream_ resource returned an error.

If you're calling an API:

- the `summary` will include the HTTP status code returned by the API
- the object may include `error.upstream_error_body`, which contains the contents of the error body received from the API

**`400`**

You made a bad request. Most commonly, you are not including required variables in your request.

**`404`**

The slug you are attempting to invoke is not registered on Decode.
