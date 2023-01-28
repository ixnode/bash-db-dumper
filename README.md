# Bash DB Dumper

[![Release](https://img.shields.io/github/v/release/ixnode/bash-db-dumper)](https://github.com/ixnode/bash-db-dumper/releases)
[![PHP](https://img.shields.io/badge/PHP-^8.0-777bb3.svg?logo=php&logoColor=white&labelColor=555555&style=flat)](https://www.php.net/supported-versions.php)
[![LICENSE](https://img.shields.io/github/license/ixnode/bash-db-dumper)](https://github.com/ixnode/bash-db-dumper/blob/master/LICENSE)

> This tool helps you to dump db fixtures from given database and can import existing db fixtures.
> Credentials and configurations are read from an .env file.

## Installation

```bash
composer require ixnode/bash-db-dumper
```

```bash
vendor/bin/db-dumper -V
```

```bash
db-dumper 0.1.0 (2023-28-01 16:19:31) - Björn Hempel <bjoern@hempel.li>
```

## Preparation

Add at least the following configuration variables to your .env file:

* `MYSQLDUMP_DATABASE_URL`
* `MYSQLDUMP_IGNORED_TABLES`

```bash
###> table-dumper (local docker settings) ###
MYSQLDUMP_DATABASE_URL=mysql://<db-user>:<db-pass>@<db-host>:<db-port>/<db-name>?serverVersion=<version>
MYSQLDUMP_IGNORED_TABLES=
###< table-dumper (local docker settings) ###
```

See `.env.dist` file for other examples and configuration variables like:

* `MYSQLDUMP_FILTERED_TABLES`
* `MYSQLDUMP_TABLES_NO_DATA`
* `MYSQLDUMP_TABLES_ONLY_DATA`

## Dump tables into db fixtures

```bash
$ bin/dbHelper dump
```

## Import existing db fixtures from `fixtures/db` into database

```bash
$ bin/dbHelper import
```

## Show help

Shows the parameters and arguments of the tool.

```bash
vendor/bin/db-dumper -h
```

```bash
db-dumper 0.1.0 (2023-28-01 16:19:31) - Björn Hempel <bjoern@hempel.li>

Usage: db-dumper [options...] dump
Usage: db-dumper [options...] import

 -e,    --env-path                    Contains the environment path (.env.local)

 -dcs,  --disable-column-statistics   Disable mysql column statistics


 -t,    --with-time                   Also outputs the time to each log entry (default: false).
 -v,    --verbose                     Set output to verbose (default: false).
 -c,    --color                       Colored output (default: false).
 -d,    --debug                       Set to debug mode. No longer performs any actions.
                                      Shows only the commands. (default: false).
 -l,    --print-log                   Print the log file
 -u,    --update-version              Shows this script with updated version read from VERSION
 -h,    --help                        Shows this help.
 -V,    --version                     Shows the version number.
```

## Use debug mode

The command only shows the commands and does not execute them:

```bash
$ bin/dbHelper dump -d
```

```bash
$ bin/dbHelper import -d
```

## Show last log

```bash
$ bin/dbHelper -l
```

## Update version

```bash
vi VERSION
```

```bash
bin/dbHelper -u > bin/dbHelper
```

## License

This tool is licensed under the MIT License - see the [LICENSE.md](/LICENSE.md) file for details
