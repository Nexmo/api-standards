---
title: "Partial Responses"
date: 2019-11-30T20:51:07+00:00
severity: may
category: properties
example_apis: []
---

You may use a `fields` parameter to filter the keys returned in an API response.

The following rules explain the supported syntax for the fields parameter value, which is loosely based on XPath syntax:

* Use a comma-separated list (fields=a,b) to select multiple fields.
* Use an asterisk (fields=*) as a wildcard to identify all fields.
* Use parentheses (fields=a(b,c)) to specify a group of nested properties that will be included in the API response.
* Use a forward slash (fields=a/b) to identify a nested property.

> As with all query parameter values, the fields parameter value must be URL encoded.

### Examples

The following examples all return the playlist ID, title and position:

* fields=items/id,playlistItems/snippet/title,playlistItems/snippet/position
* fields=items(id,snippet/title,snippet/position)
* fields=items(id,snippet(title,position))

### Why did we choose this?

This is a DRAFT proposal that has not yet been selected

### Related Links

* http://googlecode.blogspot.com/2010/03/making-apis-faster-introducing-partial.html
* http://highscalability.squarespace.com/blog/2011/3/9/google-and-netflix-strategy-use-partial-responses-to-reduce.html
* https://dev.to/andersonjoseph/what-they-want-is-what-they-get-the-partial-response-strategy-5a0m
