---
title: "HAL-JSON"
date: 2018-07-31T01:16:31+01:00
severity: must
category: response
example_apis: []
---

This is a short description of the standard

* [HAL-JSON](http://stateless.co/hal_specification.html) provides a consistent format supported by consumer and provider tooling.
* Allows resources to be embedded using an `_embedded` property (with a distinguishing key).
* Collections are resources that embed a set of resources of the same type.
* Collections are not limited to a fixed set of properties (can create collection specific properties like 'queued_calls' to provide a count of a subset).
* Related resources will be referenced under a `_links` property.
* There will always be a `_links.self` to the current resource.
* Paging will use `_links`.

> *Important:* The base URL in the `_links` section must reflect the host used for the incoming request. If the user calls `https://api-eu-1.nexmo.com` then the base URL for any `href` fields in `_links` must be the same (unless there are technical limitations why we must use `https://api.nexmo.com`)

### Examples

```json
{
  "page_size": 100,
  "page": 3,
  "_embedded": {
    "resource_name": {
        "data": "here"
    }
  },
  "_links": {
    "self": {
      "href": "https://example.com/resource?page_size=100&order=asc&page=3"
    },
    "next": {
      "href": "https://example.com/resource?page_size=100&order=asc&page=4"
    },
    "prev": {
      "href": "https://example.com/resource?page_size=100&order=asc&page=2"
    }
  }
}
```

### Why did we choose this?

Pre-existing standard

### Related Links

* [hal-draft](https://tools.ietf.org/html/draft-kelly-json-hal-07)
