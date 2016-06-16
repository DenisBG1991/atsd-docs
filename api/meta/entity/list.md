# Entities: List

## Description

## Request

### Path

```elm
/api/v1/entities
```

### Method

```
GET
```

### Headers

None.

### Parameters

None.

### Fields

|**Fields**|**Required**|**Description**|
|---|---|---|
|active|no|Filter entities by last insert time. If `active = true`, only entities with positive `last_insert_time` are included in the response|
|expression|no|Use `name` variable for entity name. Use `*` placeholder in `like` expresions|
|tags|no|Specify entity tags to be included in the response, use `tags=*` as a wildcard (returns all existing tags)|
|minInsertDate|no|return entities with lastInsertTime equal or greater than specified time, accepts iso date format|
|maxInsertDate|no|return entities with lastInsertTime less than specified time, accepts iso date format|
|limit|no|Limit response to first N entities, ordered by name.|


## Response

### Fields

| **Field**                            | **Description**                                                                             |
|---|---|
| name                                | Entity name (unique)                                                                        |
| enabled                             | Enabled status. Incoming data is discarded for disabled entities                            |
| lastInsertTime                      | Last time value was received by ATSD for this entity. Time specified in epoch milliseconds. |
 |lastInsertDate|Last time value was received by ATSD for this metric. Time specified in ISO format.|
|tags as requested by tags parameter|User-defined tags|

<aside class="notice">
If `timeFormat=iso` is set in the request, then `lastInsertDate` will be returned. If `timeFormat` is set to the default value (milliseconds), then `lastInsertTime` will be returned.
</aside>

### Errors

## Example

### Request

#### URI

```elm
GET https://atsd_host:8443/api/v1/entities?timeFormat=iso&limit=2&expression=name%20like%20%27nurs*%27
```

#### Payload

None.

#### curl

```elm
curl https://atsd_host:8443/api/v1/entities?timeFormat=iso&limit=2&expression=name%20like%20%27nurs*%27 \
  --insecure --verbose --user {username}:{password} \
  --request GET
```

### Response

```json
 [
    {
        "name": "nurswgdkr002",
        "enabled": true,
        "lastInsertDate": "2015-09-04T15:43:36.000Z"
    },
    {
        "name": "nurswgdkr002/",
        "enabled": true
    }
]
```

## Additional examples
* [List entities by name](./examples/list-entities-by-name.md)
* [List entities by maxInsertDate](./examples/list-entities-by-maxinsertdate.md)
* [List entities by minInsertDate](./examples/list-entities-by-mininsertdate.md)
* [List all tags for all entities starting with name](examples/list-all-tags-for-all-entities-with-name.md)
* [List entities by name and tag](examples/list-entities-by-tag-containing-hbase.md)




