# Properties for type 'disk' with key

## Request
### URI
```elm
POST https://atsd_host:8443/api/v1/properties/query
```
### Payload
```json
[
  {
    "type": "disk",
    "entity": "nurswgvml007",
    "key": {"id": "dm-0"}
  }
]
```

## Response

```json
[
   {
       "type": "disk",
       "entity": "nurswgvml007",
       "key": {
           "id": "dm-0"
       },
       "tags": {
           "disk_%busy": "1.6",
           "disk_block_size": "4.0",
           "disk_read_kb/s": "0.0",
           "disk_transfers_per_second": "59.5",
           "disk_write_kb/s": "238.2"
       },
       "date": "2015-02-05T16:55:02Z"
   }
]
```
