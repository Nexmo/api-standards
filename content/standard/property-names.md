---
title: "Property Names"
date: 2018-07-31T01:15:07+01:00
severity: must
category: properties
example_apis: []
---

- Have parameters / properties in lower case with underscores. 
- Have identifiers following the format: type_id. (message_id, recording_id, etc)
- Use distinguishers only when the name is non-intuitive or conflicts with another name. (`count` instead of `message_count` because message should be intuitive, but `carrier_network` if there's also a roaming network)
- Reuse parameter / property names. (`from` instead of `msisdn`)

### Examples

- `machine_detection`
- `call_id`
- `balance_transfer_id`

### Why did we choose this?

Pre-existing standard

### Related Links

N/A
