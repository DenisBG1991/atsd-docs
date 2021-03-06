# SUSE Linux Enterprise Server: rpm package

## Supported Versions

- SUSE Linux Enterprise Server 11 SP3
- SUSE Linux Enterprise Server 12.x

## Requirements

- Minimum RAM: 1 GB 
- See [Requirements](../administration/requirements.md "ATSD Requirements") for additional information.

## Connection

If the target machine does not have Internet connection to download
dependencies, use the [offline installation option](sles-offline.md).

## Download

Download rpm package to the target server:

* `curl -O https://www.axibase.com/public/atsd_ce_amd64.rpm`
* [https://axibase.com/public/atsd_ce_rpm_latest.htm](https://axibase.com/public/atsd_ce_rpm_latest.htm)

## Installation Steps

Install ATSD with dependencies:

```sh
sudo zypper -n install atsd_ce_amd64.rpm
```

It may take up to 5 minutes to initialize the database.

## Check Installation

```sh
tail -f /opt/atsd/atsd/logs/start.log                                   
```

You should see **ATSD start completed** message at the end of the start.log.

Web interface is accessible on port 8088 (http) and 8443 (https).

## Troubleshooting

* Review [troubleshooting guide](troubleshooting.md).

## Validation

* [Verify database installation](verifying-installation.md).

## Post-installation Steps

* [Basic configuration](post-installation.md).
* [Getting Started guide](/tutorials/getting-started.md).
