---
title: "Pagination"
date: 2018-07-31T01:17:04+01:00
severity: must
category: response
example_apis: []
---

APIs at Nexmo shall use one of the following pagination schemes:

* Cursor based for ever-expanding data sets, or where it's infeasible to count the total number of records e.g. Voice API call log. Cursor based pagination is also used when data is programatically added to a data set e.g.  call recordings to the Media API
* Page based for small, managed APIs where the customer is in control of what is in the data set e.g. Number pools

To the customer, having two different pagination methods is OK, as in practice they should request the first page and then follow the `_links.next` URL to get the next page.

Cursor implementation can be decided by the engineering team. Results returned must be consistently ordered, and the customer can decide if the data set is returned in ascending or descending order.

#### Cursor based

Nexmo APIs shall use a cursor as their pagination option unless otherwise agreed with DevRel.

> Cursors, if you’re not familiar, are like pointers. Pointers point at things, they reference a specific iota, a place in the list where your last request left off. A bookmark with breadcrumbs built in. (via [Slack](https://api.slack.com/docs/pagination#cursors))

- There shall be a way to page through collections without additional filters.
- There shall be a way to page through collections with filters.
- Cursors shall not expire
- Paging shall use a standard set of hal+json `_links`
  - `self` (current page, required)
  - `next` (next page, optional)
  - `prev` (previous page, optional)
  - `first` (first page, required)
- Paging `_links` must include filters.
- The page size parameter must be called `page_size`
- The cursor parameter must be called `cursor`

#### Page Based

In certain situations (e.g. purchasing a number) it may be beneficial to skip
over pages if you're not interested in that data. In this situation, `page` and
`page_size` shall be used.

The first page is page `1`.

To add a new page-based public API, you must get agreement from DevRel.

- Paging shall use a standard set of hal+json `_links`
  - `self` (current page, required)
  - `next` (next page, optional)
  - `prev` (previous page, optional)
  - `first` (first page, required)
  - `last` (last page, required)
- Paging `_links` must include filters.
- The page size parameter must be called `page_size`
- The page index parameter must be called `page`
- The page count parameter must be called `total_pages`
- The results parameter must be called `total_items`

### Examples

#### Cursor

```json
{
  "page_size": 100,
  "_embedded": {
    "users": [
      {
        "id": "abc123",
        "name": "Ashley"
      }
    ]}
  },
  "_links": {
    "self": {
      "href": "https://example.com/resource?page_size=100&order=asc&cursor=19284743"
    },
    "next": {
      "href": "https://example.com/resource?page_size=100&order=asc&cursor=19291731"
    },
    "prev": {
      "href": "https://example.com/resource?page_size=100&order=asc&cursor=19283018"
    }
  }
}
```

#### Page

```json
{
  "page_size": 100,
  "page": 3,
  "total_pages": 8,
  "total_items": 814,
  "_embedded": {
    "users": [
      {
        "id": "abc123",
        "name": "Ashley"
      }
    ]
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
    },
    "last": {
      "href": "https://example.com/resource?page_size=100&order=asc&page=8"
    }
  }
}
```

### Why did we choose this?

#### Cursor

* It's more efficient for large data sets as you don't need to calculate the full set size to start returning data
* If items are removed in an earlier page, data will not be missed

#### Page

* Some APIs are better suited to page based searching, particularly those where you want to jump around the data set e.g. number pools or the number catalog (where you may want to skip a certain prefix by skipping multiple pages at a time)

### Related Links

* [Evolving pagination at Slack](https://slack.engineering/evolving-api-pagination-at-slack-1c1f644f8e12)
* [Facebook Graph API](https://developers.facebook.com/docs/graph-api/using-graph-api/#paging)
