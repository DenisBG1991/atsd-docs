# Ubuntu/Debian: Debian Package

## Supported Versions

- Ubuntu 14.04
- Ubuntu 16.04
- Debian 6.x
- Debian 7.x

## Requirements

- Minimum RAM: 1 GB 
- See [Requirements](../administration/requirements.md "ATSD Requirements") for additional information.

## Check Connection

If the target machine is not connected to public repositories to install dependencies with APT, 
use the [offline installation option](ubuntu-debian-offline.md).

## Download

Download deb package to the target server:

* `wget https://www.axibase.com/public/atsd_ce_amd64.deb`
* [https://axibase.com/public/atsd_ce_deb_latest.htm](https://axibase.com/public/atsd_ce_deb_latest.htm)

## Installation Steps

#### Add `openjdk` Repository

This step is required **only on Ubuntu 16.04** (Xenial Xerus).

```sh
sudo add-apt-repository ppa:openjdk-r/ppa  
```

#### Update repositories and install dependencies

```sh
sudo apt-get update && sudo apt-get install -y openjdk-7-jdk sysstat curl hostname
```

> If there are any issues with installing the dependencies, [check the repositories](modifying-ubuntu-debian-repositories.md "Modifying Repositories") and retry the command.

#### Follow the prompts to install ATSD

```sh
sudo dpkg -i atsd_ce_amd64.deb
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
