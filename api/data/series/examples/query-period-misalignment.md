# Series Query: Period Misalignment

## Description

If the time range between startDate and endDate cannot be filled with a whole number of periods, some of the periods will contain a subset of data and some of the period will be excluded from resultset because their start time will be before startDate.

The below query produced no data because:

1. With the default `CALENDAR` alignment, the 1-minute periods overlapping the time range are: `[14:20:00-14:21:00)` and `[14:21:00-14:22:00)`
2. `[14:20:00-14:21:00)` period has 4 samples as provided below, but its start time is before the `startDate`.
3. `[14:21:00-14:22:00)` period's start time is within the time range (period's start time is before `endDate`) however the detailed data for this period was limited with `endDate` of `14:22:01` and the period doesn't have any samples as a result. 

## Request

### URI

```elm
POST https://atsd_host:8443/api/v1/series/query
```

### Payload

```json
[
  {
    "startDate": "2016-06-27T14:20:01Z",
    "endDate":   "2016-06-27T14:21:01Z",
    "entity": "nurswgvml007",
    "metric": "cpu_busy",
    "aggregate": {"period": {"count": 1, "unit": "MINUTE"},
                  "type": "COUNT"}
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
      "type": "COUNT",
      "period": {
        "count": 1,
        "unit": "MINUTE",
        "align": "CALENDAR"
      }
    },
    "data": []
  }
]
```

## Detailed Data

```ls
| datetime                 | value | 
|--------------------------|-------| 
| 2016-06-27T14:20:04.000Z | 9.1   | 
| 2016-06-27T14:20:20.000Z | 37.5  | 
| 2016-06-27T14:20:36.000Z | 7.2   | 
| 2016-06-27T14:20:52.000Z | 22.0  | 
```


