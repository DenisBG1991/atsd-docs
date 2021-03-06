# Metric: Create or Replace

## Description 

Create a metric with specified properties and tags or replace an existing metric.

If the metric exists, all of its current properties and tags will be overwritten with fields specified in the request.

In order to update only specific fields specified in the request, use [Metric: Update](update.md) method.

## Request

### Path

```elm
/api/v1/metrics/{metric}
```

### Method

```
PUT
```

### Headers

|**Header**|**Value**|
|:---|:---|
| Content-Type | application/json |

### Parameters

None.

### Fields

Refer to Fields specified in [Metrics List](list.md#fields) method.

## Response

### Fields

None.

### Errors

None.

## Example

### Request

#### URI

```elm
PUT https://atsd_host:8443/api/v1/metrics/my-metric
```

#### Payload

```json
{
  "enabled": true,
  "persistent": true,
  "dataType": "DOUBLE",
  "timePrecision": "MILLISECONDS",
  "retentionInterval": 0
}
```

#### curl

```elm
curl https://atsd_host:8443/api/v1/metrics/my-metric \
  --insecure --verbose --user {username}:{password} \
  --header "Content-Type: application/json" \
  --request PUT \
  --data '{"enabled":true,"persistent":true,"dataType":"DOUBLE","timePrecision":"MILLISECONDS","retentionInterval":0}'
```

### Response

None.

## Additional Examples
