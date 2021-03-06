# CSV File Upload

## Description

Upload CSV file or multiple CSV files for parsing into series, properties, or messages with the specified CSV parser.

File(s) can be optionally compressed with gzip or zip. 

Multiple files can be archived with zip/tar and uploaded as one zip or tar.gz archive.

The method supports processing of the uploaded file attached as data as well as a part in multi-part payload.

## Request

| **Method** | **Path** |
|:---|:---|
| POST | `/api/v1/csv` |

### Headers

File Data mode:

|**Header**|**Value**|
|:---|:---|
| Content-Type | `text/csv` - for plain text CSV file.<br>`application/zip` - for compressed zip file and archive (**.zip**)<br>`application/gzip` or `application/x-gzip` - for compressed gzip file (**.gz**) or archive (**.tar.gz**).|

Multi-part mode:

|**Header**|**Value**|
|:---|:---|
| Content-Type | `multipart/*`, for example `multipart/form-data` or  `multipart/mixed`. <br>Content type for the file part itself should be set as described in File Data mode above.|

### Query String Parameters

| **Field** | **Type** | **Description** |
|:---|:---|:---|
| config   | string   | [**Required**] Parser Name as configured on **Configuration:Parsers CSV** page.|
| encoding      | string   | File encoding. Default: UTF-8.|
| filename      | string   | [**Required** for archived files uploaded in File Data mode] <br>Name of the file or archive being sent, for example text.csv, files.zip, files.tar.gz.<br>The archive may contain multiple files, all of which will be processed.<br>Archive compression is determined based on file extension.<br>Supported archive formats: zip and tar.gz.<br>Supported file extensions for the uploaded archive: .gz, .tar.gz, .zip.  |
| default-entity| string | Default entity name applied to commands contained in the file. |
| metric-prefix | string | Prefix added to all metric names extracted from the file. |
| wait | boolean | Wait until processing of the file into commands is completed by the server. Default: false.<br>If wait is disabled, the file is processed by the server asynchronously. | 
| rules | boolean | Process commands in the rule engine. Default: false | 
| time | string | Date in ISO 8601 format, applied to commands if the file doesn't contain any time columns. | 
| timezone | string | Timezone applied to timestamps specified in local time. | 
| test | boolean | Parse and validate the file without actually processing and storing commands. Default: false. | 

### Payload

* File attached as data, or
* Multi-part content containing the file. Part name containing the uploaded file should be named `filedata` and include `filename` parameter:

```
Content-Disposition: form-data; name="filedata"; filename="arch.tar.gz"
```

## Response 

### Fields

None.

### Errors

## Processing

* Names (metric name, property type, key names, tag names) containing non-printable characters will be normalized by replacing them with underscore.

## Example 

### Request 

#### URI

```elm
POST https://atsd_host:8443/api/v1/csv?config=my-parser&default-entity=nurswgvml007
```

#### Payload

```ls
time,cpu_user,cpu_system,waitio
1423139581000,12.4,1.4,0
1423139592016,16.0,4.2,0
```

### Response

None.

## Additional Examples

### curl upload

```sh
curl -i -user admin:pwd -F filedata=@test.tar.gz http://atsd_host:8088/api/v1/csv?config=noc-parser
```


