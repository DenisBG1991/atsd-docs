# Monitoring metrics : JSON

Retrieve ATSD and HBase JMX metrics and outputs in JSON:

| Method Name | URL | Response |
| --- | --- | --- |
| ATSD | http://atsd_server.com:8088/jmx | [atsd.json](sources/atsd.json) |
| Hbase Region Server | http://atsd_server:60030/jmx | [hbase-region-server.json](sources/hbase-region-server.json) |
| Hbase Master | http://atsd_server:60010/jmx | [hbase-master.json](sources/hbase-master.json) |