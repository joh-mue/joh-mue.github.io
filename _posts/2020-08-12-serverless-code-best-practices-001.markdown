---
title: Serverless Code Best Practices #001
date:   2020-08-12 14:00:00 +0100
tags: programming, python, serverless
layout: post
---

## Instead of documenting event content as a comment, unpack your event at the top of the handler

Instead of documenting which structure your incoming event should have, unpack it straight away. This way the documentation won't age or become obsolete and you are automatically separating the Lambda handler from your core logic.

### BAD

```python
"""
{
  "Input": 1585620000,
  "contract_id": "Hour H-2020-033104",
  "received_timestamp_start": 1585607624738,
  "received_timestamp_stop": 1585607685738,
  "received_odb_start": "30/03/2020 22-33-44",
  "received_odb_stop": "30/03/2020 22-34-45",
  "username": "EMA",
  "password": "EMA-EPEX",
  "dsn": "nexxt-oracledb-prod.c1xbvqjqzrvx.eu-central-1.rds.amazonaws.com:1521/NEXXTDBP"
}
"""


def handler(event, context):
  
  #...
```

### GOOD

```python
def handler(event, context):
  
  Input = event["Input"]
  contract_id = event["contract_id"]
  received_timestamp_start = event["received_timestamp_start"]
  received_timestamp_stop = event["received_timestamp_stop"]
  received_odb_start = event["received_odb_start"]
  received_odb_stop = event["received_odb_stop"]
  username = event["username"]
  password = event["password"]
  dsn = event["dsn"]

  #...
```
