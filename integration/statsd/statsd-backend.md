# StatsD Backend

ATSD backend for StatsD enables you to forward metrics collected by StatsD daemon into Axibase Time-Series Database for retention, analytics, visualization, and alerting.

[Learn more about StatsD.](https://axibase.com/products/axibase-time-series-database/writing-data/statsd/)

[Download the ATSD StatsD backend.](https://github.com/axibase/atsd-statsd-backend)

#### Configuration

Configuration file example:

```json
{
    atsd: {
        host: "192.168.1.233",
        port: 8082,
        protocol: "udp",
        patterns: [
            {
                pattern: "alfa\\..*\\.charlie\\..*$",
                atsd_pattern: "<entity>.<>.<tag:test>.<metric>"
            }
        ]
    },
    port: 8125,
    backends: [
        "./backends/atsd"
    ],
    debug: true
}
```
Possible variables:

| Variable | Description | Default Value | 
| --- | --- | --- | 
|  <p>debug</p>  |  <p>enable debug logging : `true` or `false`</p>  |  <p>`false`</p>  | 
|  <p>keyNameSanitize</p>  |  <p>sanitizing metric names (removing forbidden characters): `true` or `false`</p>  |  <p>`true`</p>  | 
|  <p>flush_counts</p>  |  <p>processing flush counts: `true` or `false`</p>  |  <p>true</p>  | 
|  <p>atsd</p>  |  <p>container for all backend-specific options</p>  |  <p>–</p>  | 
|  <p>atsd.host</p>  |  <p>ATSD hostname</p>  |  <p>–</p>  | 
|  <p>atsd.port</p>  |  <p>ATSD port</p>  |  <p>8081</p>  | 
|  <p>atsd.user</p>  |  <p>username</p>  |  <p>“”</p>  | 
|  <p>atsd.password</p>  |  <p>password to log into ATSD</p>  |  <p>“”</p>  | 
|  <p>atsd.protocol</p>  |  <p>protocol: `"tcp"` or `"udp"`</p>  |  <p>“tcp”</p>  | 
|  <p>atsd.entity</p>  |  <p>default entity</p>  |  <p>local hostname</p>  | 
|  <p>atsd.prefix</p>  |  <p>global prefix for each metric</p>  |  <p>“”</p>  | 
|  <p>atsd.prefixCounter</p>  |  <p>prefix for counter metrics</p>  |  <p>“counters”</p>  | 
|  <p>atsd.prefixTimer</p>  |  <p>prefix for timer metrics</p>  |  <p>“timers”</p>  | 
|  <p>atsd.prefixGauge</p>  |  <p>prefix for gauge metrics</p>  |  <p>“gauges”</p>  | 
|  <p>atsd.prefixSet</p>  |  <p>prefix for set metrics</p>  |  <p>“sets”</p>  | 
|  <p>atsd.patterns</p>  |  <p>patterns to parse statsd metric names</p>  |  <p>–</p>  | 


[Other variables used by StatsD can be specified.](http://github.com/etsy/statsd/blob/master/exampleConfig.js')

StatsD has an [open bug](https://github.com/etsy/statsd/issues/462) regarding the inability for configuration to sometimes reload during operation. Changing the configuration file while StatsD is running, may result in StatsD crashing. Until the bug is fixed, add `automaticConfigReload: false` to your configuration, restart StatsD for the changed configuration to take effect.

#### Patterns

Patterns enable the conversion of native StatsD metric names into ATSD entity/metric/tags.

If a metric name matches regexp `pattern`, it will be parsed according to `atsd_pattern`.

> NOTE: every `\` in `pattern` must be duplicated.

If a metric name has more tokens than `atsd_pattern`, extra tokens are cropped.

`alfa.bravo.charlie.delta` is used as an example metric and the default example entity is `zulu`.

`metric` – metric token; multiple occurrences are combined


`entity` – entity token to replace the default entity; multiple occurrences are combined

```
[garbageCollections]
pattern = garbageCollections$
atsd-pattern = <tag:type>.<tag:dep>.<entity>.<metric>.<metric>.<metric>

# atsd-pattern = <tag:type>.<tag:dep>.<entity>.<metrics>     -Alternative Syntax
```

`tag:tag_name` – token for the tag named `tag_name`

```
atsd-pattern = <entity>.<tag:test>.<metric>.<metric>
result = series e:alfa m:charlie.delta t:test=bravo ...
```

`metrics` – any number of metric tokens; can be used once per pattern; can also be omitted

```sh
atsd-pattern = <entity>.<tag:test>.<metrics>
result = series e:alfa m:charlie.delta t:test=bravo ...
```

```
<> - token to be excluded
atsd-pattern = <entity>.<tag:test>.<>.<metric>
result = series e:alfa m:delta t:test=bravo ...
```
