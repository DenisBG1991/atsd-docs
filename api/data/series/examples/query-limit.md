# Series Query: Apply Limit to Results

## Description

Number of samples (time:value) returned for each series can be limited with `limit` parameter.

The limit applies to each series separately.

Samples for each series are always sorted by time in ascending order.

`limit` of N returns last N values.

## Request

### URI

```elm
POST https://atsd_host:8443/api/v1/series/query
```

### Payload

```json
[
    {
        "startDate": "2016-02-22T13:30:00Z",
        "endDate":   "2016-02-22T13:31:00Z",
        "entity": "nurswgvml007",
        "metric": "cpu_busy",
		"limit": 1
    }
]
```

## Response

### Payload

```json
[
  {
    "entity": "nurswgvml007",
    "metric": "cpu_busy",
    "tags": {},
    "type": "HISTORY",
    "aggregate": {
      "type": "DETAIL"
    },
    "data": [
      {
        "d": "2016-02-22T13:30:56.000Z",
        "v": 4
      }
    ]
  }
]
```


