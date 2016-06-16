# Ubuntu/Debian: APT

## Supported Versions

- Ubuntu 14.04
- Ubuntu 16.04
- Debian 6.x
- Debian 7.x

## Requirements

- Minimum RAM: 1 GB 
- See [Requirements](../administration/requirements.md "ATSD Requirements") for additional information.

## Installation Steps

#### Add openjdk Repository

This step is required **only on Ubuntu 16.04** (Xenial Xerus).

```sh
sudo add-apt-repository ppa:openjdk-r/ppa  
```

#### Update repositories

```sh
sudo apt-get update
```

#### Add `axibase.com/public/repository/deb/` repository

```sh
sudo apt-key adv --keyserver hkp://keyserver.ubuntu.com:80 \
--recv-keys 26AEE425A57967CFB323846008796A6514F3CB79                             
```

```sh
sudo sh -c 'echo "deb [arch=amd64] http://axibase.com/public/repository/deb/ ./" \
>> /etc/apt/sources.list.d/axibase.list'
```

#### Update repositories and follow the prompts to install ATSD

```sh
sudo apt-get update && sudo apt-get install atsd                       
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
