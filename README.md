# Axibase Time Series Database Documentation


* Installation
    * [Requirements](administration/requirements.md)
    * [Distributions](installation#installation-guides)
* [API](api)
    * [Data](api/data#overview)
      * Series
      * Properties
      * Messages
      * Alerts
    * [Meta](api/meta#overview)
      * Metrics
      * Entities
      * Entity Groups
    * [Network](api/network#network-api)
      * series
      * property
      * message
      * csv
      * nmon
    * [SQL](api/sql#overview)   
* [API Clients](api#api-clients)
    * [R](https://github.com/axibase/atsd-api-r)
    * [PHP](https://github.com/axibase/atsd-api-php)
    * [Java](https://github.com/axibase/atsd-api-java)
    * [Python](https://github.com/axibase/atsd-api-python)
    * [Ruby](https://github.com/axibase/atsd-api-ruby)
    * [NodeJS](https://github.com/axibase/atsd-api-nodejs)
* Drivers
    * [JDBC](https://github.com/axibase/atsd-jdbc)
* Rule Engine
    * [Overview](rule-engine/rule-engine.md)
    * [Expression](rule-engine/expression.md)
    * [Functions](rule-engine/functions.md)
    * [Placeholders](rule-engine/placeholders.md)
    * [Email Action](rule-engine/email-action.md) 
* Integration
    * [ActiveMQ](integration/activemq#monitoring-activemq-with-atsd)
    * [Axibase Enterprise Reporter](integration/aer#atsd-adapter)
    * [IBM Tivoli Monitoring](integration/itm#ibm-tivoli-monitoring)
    * [Derby] (https://github.com/axibase/axibase-collector-docs/tree/master/jobs/examples/derby#overview)
    * [HP Openview](https://github.com/axibase/axibase-collector-docs/tree/master/jobs/examples/hp-openview#overview)
    * [Jetty](https://github.com/axibase/axibase-collector-docs/tree/master/jobs/examples/jetty#overview)
    * [JVM](https://github.com/axibase/axibase-collector-docs/tree/master/jobs/examples/jvm#overview)
    * [MySQL Server](https://github.com/axibase/axibase-collector-docs/tree/master/jobs/examples/mysql#overview)
    * [NGINX](https://github.com/axibase/axibase-collector-docs/tree/master/jobs/examples/nginx#overview)
    * [Oracle Enterprise Manager](https://github.com/axibase/axibase-collector-docs/tree/master/jobs/examples/oracle-enterprise-manager#overview)
    * [PostgreSQL](https://github.com/axibase/axibase-collector-docs/tree/master/jobs/examples/postgres#overview)
    * [Microsoft System Center Operations Manager](https://github.com/axibase/axibase-collector-docs/tree/master/jobs/examples/scom#overview)
    * [SolarWinds](https://github.com/axibase/axibase-collector-docs/tree/master/jobs/examples/solarwinds#overview)
    * [Tomcat Servlet Container](https://github.com/axibase/axibase-collector-docs/tree/master/jobs/examples/tomcat#overview)
    * [VMware](https://github.com/axibase/axibase-collector-docs/tree/master/jobs/examples/vmware#overview)
* [Administration](administration#administration)
    * [Deployment](administration/deployment.md)
    * [Setting up the Email Client](administration/setting-up-email-client.md)
    * [User Authentication](administration/user-authentiication.md)
    * [User Authorization](administration/user-authorization.md)
    * [Restarting](administration/restarting.md)
    * [Updating](administration/update.md)
    * [Uninstalling](administration/uninstalling.md)
    * [Migrate ATSD to Java 7](administration/migrate-to-java7.md)
    * [Network Settings](administration/networking-settings.md)
    * [Enabling Swap Space](administration/enabling-swap-space.md)
    * [Enabling Replication](administration/replication.md)
    * [Allocating Memory to components](administration/allocating-memory.md)
    * [Changing the Directory Where Data is Stored](administration/changing-data-directory.md)
    * [Editing Configuration Files](administration/editing-configuration-files.md)
    * [Logging](administration/logging.md)
    * [Metric Persistence Filter](administration/metric-persistence-filter.md)
    * [Entity Lookup](administration/entity-lookup.md)
    * [Restoring a corrupted zookeeper](administration/entity-lookup.md)
    * [Compaction](administration/compaction.md)
    * [Compaction Test](administration/compaction-test.md)
    * [Monitoring](administration/monitoring.md)