# SQL Scheduler

## Overview

SQL Scheduler allows for SQL query results to be distributed to email subscribers or stored on a local file system in CSV, Excel or JSON format.

![Scheduler Example](sql-scheduler-example.png)

## Query

The scheduler can execute a SELECT query as described in the [overview](README.md).

## Authorization

The SQL queries are executed with administrative permissions and no records are excluded from the resultset unlike adhoc queries which are filtered based on user's entity permissions.

## Schedule

The scheduling frequency is controlled with `Schedule` field containing a `cron` expression that determines when the task should be executed.

Fields in a cron expression have the following order:

* seconds
* minutes
* hours
* day-of-month
* month
* day-of-week
* year **(optional)**

For example, `0 0 8 * * ? *`, means the query will be executed at 08:00:00 every day.

![Cron Expressions](http://axibase.com/wp-content/uploads/2016/03/cron_expressions.png)

_*Either '0' or '7' can be used for Sunday in the day-of-week field._

cron Expression Examples:

**Expression** | **Description**
:---|:---
`0/10 * * * * ?` | Every 10 seconds.
`0 0/15 * * * ?` | Every 15 minutes.
`0 * * * * ?` | Every minute.
`0 0 0 * * ?` | Every day at 0:00.  
`0 5,35 * * * ?` | Every hour at 5th and 35th minute.

## Formats

* CSV
* JSON
* Excel (xlsx)

CSV files can be optionally archived with zip or gzip compression.

### Sample Reports

* [sql-report.csv](examples/sql-report.csv)
* [sql-report.json](examples/sql-report.json)
* [sql-report.xlsx](examples/sql-report.xlsx)

## Decimal Precision

To round numeric values, set decimal precision to the desired number of fractional digits.
`0` means that no fractional digits will be displayed.
`-1` means that no rounding will be applied and numbers will be displayed in their native representation.

## Export Options

The report file can be stored in a file on the server or sent to email subscribers.

### File System

Specify absolute path including file name on the server to which the report will be stored.
If the parent directory in the specified path doesn't exist, it will be automatically created.
File name should match the file format. For example, if format is EXCEL, Output Path should end with ".xlsx".

Output Path may contain date placeholders so that files or their parent directories are grouped by day or month.

Example: `/opt/report/daily/${yyyy-MM-dd}.csv`

An expression like `/opt/report/daily/${yyyy-MM-dd}.csv` creates the following directory `/opt/report/daily/2016-06-10.csv` when executed.

* yyyy - 4-digit year
* yy - 2-digit year
* MM - 2-digit numeric month
* dd - day of month
* HH - hour of the day in 24-hour format
* ss - seconds
* SSS - milliseconds

### Email

To distribute report files via email specify message subject and one or multiple email addresses, separated by comma or space.

## Versioning

Selecting versioning columns (version_tatus, version_source, version_time) is  currently not supported.

## Metadata

The exported files can optionally include metadata fields about the report.
The metadata section is located in the header is prepended with hash symbol `#` and includes the following fields in "name,value" format

|**Name**|**Description**|
|:---|:---|
|publisher| Name of the reporting product (ATSD) and its URL|
|created| Date when the report was produced in ISO 8601 format|
|title | Report name, such as "CPU Busy Daily Report" |
|command | Query statement, possible on multiple lines |

In addition, the metadata header contains a list of column names in resultset and their data types.

```
#name,entity,Average,...
#datatype,string,double,...
```

### Specifications

* Axibase Time Series Database [Ontology](atsd.jsonld) in jsonld format according to [RFC6350](https://tools.ietf.org/html/rfc6350)
* W3C Recommendation [Metadata Vocabulary for Tabular Data](https://www.w3.org/TR/tabular-metadata/)

### Metadata in CSV Format

Since results produced by the task must be included in one file, it is not possible to incorporate metadata in JSON format into a CSV file.
Instead, when enabled, metadata included in the output file as part of the header with hash symbol (`#`) used as a comment symbol.

```
#publisher,Axibase Time-Series Database,https://nur.axibase.com
#created,2016-06-12T15:56:39.106Z
#title,SQL Query
#comment,"SELECT entity, avg(value) AS 'Average', median(value), max(value), count(*)  
#FROM cpu_busy 
#  WHERE time BETWEEN previous_day and current_day 
#  GROUP BY entity 
#  ORDER BY avg(value) DESC"
#name,entity,Average,median(value),max(value),count(*)
#datatype,string,double,double,double,double
entity,Average,median(value),max(value),count(*)
nurswgvml006,18.4,4.0,100.0,5385.0
```

### Metadata in Excel Format

Same as in CSV format.

### Metadata in JSON Format

Metadata is specified according to W3C Recommendation [Metadata Vocabulary for Tabular Data](https://www.w3.org/TR/tabular-metadata/)

Table schema object provides the following information about the columns in the result set:

* index, starts with 1
* name
* label (alias)
* datatype
* table name (metric name)
* type as specified in [ontology](atsd.jsonld)
* description

```json
{
	"metadata": {
		"@context": ["http://www.w3.org/ns/csvw", {
			"atsd": "http://www.axibase.com/schemas/2015/11/atsd.jsonld#"
		}],
		"dc:created": {
			"@value": "2016-06-13T08:41:25.451Z",
			"@type": "xsd:date"
		},
		"dc:publisher": {
			"schema:name": "Axibase Time-Series Database",
			"schema:url": {
				"@id": "https://nur.axibase.com"
			}
		},
		"dc:title": "SQL Query",
		"rdfs:comment": "SELECT entity, datetime, metric, avg(value) AS 'Average'  \r\nFROM cpu_busy \r\n  WHERE datetime > current_minute \r\n  GROUP BY entity, period(1 minute) \r\n  ORDER BY avg(value) DESC",
		"@type": "Table",
		"url": "sql.csv",
		"tableSchema": {
			"columns": [{
				"columnIndex": 1,
				"name": "entity",
				"titles": "entity",
				"datatype": "string",
				"table": "cpu_busy",
				"propertyUrl": "atsd:entity"
			}, {
				"columnIndex": 2,
				"name": "datetime",
				"titles": "datetime",
				"datatype": "xsd:dateTimeStamp",
				"table": "cpu_busy",
				"propertyUrl": "atsd:datetime",
				"dc:description": "Sample time in ISO8601 format"
			}, {
				"columnIndex": 3,
				"name": "metric",
				"titles": "metric",
				"datatype": "string",
				"table": "cpu_busy",
				"propertyUrl": "atsd:metric"
			}, {
				"columnIndex": 4,
				"name": "Average",
				"titles": "avg(value)",
				"datatype": "double",
				"table": "cpu_busy",
				"propertyUrl": "atsd:avg"
			}]
		}
	},
	"data": []
}
```




