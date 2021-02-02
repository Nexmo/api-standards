---
title: "Errors"
date: 2018-07-31T01:16:19+01:00
severity: must
category: response
example_apis: []
---

> All error codes should correspond to a single error condition. If you find yourself using the word `or` in an error message, it should probably be multiple error codes

Any non 200 response body should follow a standard format. This should be consistent for all products, as an error may be product specific (invalid parameters) or global in nature (invalid authorization). The [HTTP Problem draft](https://tools.ietf.org/html/draft-ietf-appsawg-http-problem-02), specifically the JSON Object provide a familiar format used by other APIs that provides a set of standard properties while allowing additional properties when needed for a particular error condition.

### Examples

In the following examples:

* `type` is both the identifier for the specific error (URI) and a link to human readable documentation about the problem.
* `code` is the fragment of the `type` for easy usage and propagation in code.
* `title` is a short indication of what went wrong 
* `detail` provides more information about the error
* `instance` is the Nexmo trace ID (previously returned as a header)

`type`, `title` and `instance` are all required fields

```
HTTP/1.1 403 Forbidden
Content-Type: application/problem+json
Content-Language: en

{
    "type": "https://example.com/Error#out-of-credit",
    "type-code": "out-of-credit",
    "title": "You do not have enough credit",
    "instance": "<trace_id>"
}
```

In some cases, you may wish to add additional detail to the error by adding a `detail` key

```
HTTP/1.1 403 Forbidden
Content-Type: application/problem+json
Content-Language: en

{
  "type": "https://example.com/Error#out-of-credit",
  "title": "You do not have enough credit",
  "type-code": "out-of-credit",
  "detail": "Your current balance is 30, but that costs 50.",
  "instance": "<trace_id>"
}
```

If there are lots of errors, you may choose to return them as structured data. In this case, you would not return `detail`, but instead add a new key at the top level and put the data inside that (see below for a list of additional keys). In this case, we're returning a set of validation errors:

```
HTTP/1.1 400 Bad Request
Content-Type: application/problem+json
Content-Language: en

{
  "type": "https://example.net/validation-error",
  "type-code": "validation-error",
  "title": "Your request parameters didn't validate.",
  "instance": "<trace_id>",
  "invalid_parameters": [
    {
      "name": "age",
      "reason": "must be a positive integer"
    },
    {
      "name": "color",
      "reason": "must be 'green', 'red' or 'blue'"
    }
  ]
}
```

To keep things consistent across APIs only the following additional keys are available:

##### invalid_parameters

Used for validation errors to provide more information about the failure

```json
"invalid_parameters": [
    {"name": "name","reason": "is required"},
    {"name": "age","reason": "must be a positive integer"}
]
```

### Why did we choose this?

It's an existing RFC. API consumers will be familiar with the format and existing tooling is available for working with the format

### Related Links

* [RFC7807](https://tools.ietf.org/html/rfc7807)
