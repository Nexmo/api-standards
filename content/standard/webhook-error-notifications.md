---
title: "Webhook Error Notifications"
date: 2011-11-22T11:15:27+01:00
severity: should
category: callbacks
example_apis: []
---

### Webhooks as Error Notifications

When sending error information as a webhook, these are our standard fields.

* `reason` (**required**): Description of the error
* `timestamp` (**required**): Timestamp in ISO 8601 format
* `level` (**required**): One of "error", "warn" or "info" - if this field is omitted, "error" should be assumed (the Voice API originally only had one error level).
* `type` (**required**): A URL to more information about the error (as used in Response Errors)
* `detail`: Any more information about the error (as used in Response Errors)

In addition, any other identifiers or other information that are useful in the error context. For example, Voice API also returns `conversation_uuid`.

#### Notes

Standard field naming guidelines for webhooks also apply.
