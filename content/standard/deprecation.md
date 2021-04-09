---
title: "Deprecation"
date: 2018-07-31T01:17:16+01:00
severity: should
category: versioning
example_apis: []
---

When the decision has been taken to deprecate an API:

* For beta products the deprecation period must be at least 30 days (60 days recommended)
* For GA products the deprecation period must be at least 1 year
* Warning emails will be sent to the API at regular intervals before the deprecation time
* A guide will be supplied to customers explaining how to migrate to the replacement API with the initial deprecation notice.
* Fields and routes that are being deprecated should be marked as such in the OpenAPI spec, but not removed until the deprecation period has elapsed. This is done by setting `deprecated: true` on the deprecated object.


### Why did we choose this?

#### Beta:

Discussed in #api-standards due to the messaging/workflows release.

Participants:

* Aristoula Goulia
* Hugh Hopkins
* Michael Heap

#### Non-Beta

Pre-existing standard

### Related Links

N/A

