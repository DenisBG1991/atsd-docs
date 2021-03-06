# Extended Commands

ATSD supports the following thirt-party line protocols:

## tcollector

```css
put `<metric> <timestamp> <value> <tagk1=tagv1[ tagk2=tagv2 ...tagkN=tagvN]>`
```

```css
put sys.cpu.user 1356998400 42.5 host=webserver01 cpu=0
```

[tcollector integration](https://axibase.com/products/axibase-time-series-database/writing-data/tcollector/)

ATSD uses the `host` tag as the entity, if `host` tag is missing then entity will be `tcollector`.

## Graphite

```css
servers.nurswgvml007.cpu_busy 24.5 1232312313
```

[Graphite integration](http://axibase.com/products/axibase-time-series-database/writing-data/graphite-format/)

## StatsD

```css
cpu.busy:20.5|c
```

```css
nurswfvml007/cpu.busy:20.5|c
```

```css
nurswgvml007.disk_used_percent:24.5|c|@0.5|#mount_point:/,disk_name:/sda
```

[StatsD integration](http://axibase.com/products/axibase-time-series-database/writing-data/statsd/)

Forward slash is supported as a control character to extract entity name. 

If no entity name is set, the default entity will be set as `statsd`.







