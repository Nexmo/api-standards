---
title: "Webhooks"
date: 2018-07-31T01:15:27+01:00
severity: should
category: callbacks
example_apis: []
---

### Delivering Data with a Webhook

`POST` is our preferred method when delivering data via webhook.

Objects and data *sent* via webhooks by the API are in `snake_case`.

#### Examples

[Voice API webhooks](https://developer.nexmo.com/voice/voice-api/webhook-reference)

* `conversation_uuid`
* `start_time`

[Messages API callbacks](https://developer.nexmo.com/api/messages-olympus#inbound-message)

* `message_uuid`
* `timestamp`

### Webhooks to Fetch Data

There may be some use cases when the webhook fetches data and causes no effect on the receiving side. In this case, `GET` method may be used and `camelCase` variables may be preferred for consistency with other parts of the application.

#### Examples

Nexmo Call Control Objects ([NCCO](https://developer.nexmo.com/voice/voice-api/ncco-reference)) examples:

* `eventUrl`
* `musicOnHold`
* `beepOnStart`

### Why did we choose this?

Pre-existing standard

### Related Links

N/A
