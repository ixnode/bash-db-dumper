# Bash DB Dumper

[![Release](https://img.shields.io/github/v/release/ixnode/bash-db-dumper)](https://github.com/ixnode/bash-db-dumper/releases)
[![PHP](https://img.shields.io/badge/PHP-^8.0-777bb3.svg?logo=php&logoColor=white&labelColor=555555&style=flat)](https://www.php.net/supported-versions.php)
[![LICENSE](https://img.shields.io/github/license/ixnode/bash-db-dumper)](https://github.com/ixnode/bash-db-dumper/blob/master/LICENSE)

> This tool helps you to dump db fixtures from given database and can import existing db fixtures.
> Credentials and configurations are read from an .env file.

## Installation

### Within a PHP project ([composer](https://getcomposer.org/))

```bash
composer require --dev ixnode/bash-db-dumper
```

```bash
vendor/bin/db-dumper -V
```

```bash
db-dumper 0.1.1 (2023-28-01 18:07:16) - Björn Hempel <bjoern@hempel.li>
```

### Outside the project

```bash
git clone git@github.com:ixnode/bash-db-dumper.git && cd bash-db-dumper
```

```bash
bin/db-dumper -V
```

```bash
db-dumper 0.1.1 (2023-28-01 18:07:16) - Björn Hempel <bjoern@hempel.li>
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
* `MYSQLDUMP_VIEWS`


# MySQL dump settings: Views will be imported after importing all tables to be sure all needed tables are exists
#
# Example: MYSQLDUMP_VIEWS=view_1,view_2
#=

### Overview of configuration

| Variable                                    | Description                                                                                                                                             | Example                                                                   |
|---------------------------------------------|---------------------------------------------------------------------------------------------------------------------------------------------------------|---------------------------------------------------------------------------|
| `MYSQLDUMP_DATABASE_URL`                    | Contains the database credentials.                                                                                                                      | `mysql://user:pass@localhost:3306/db?serverVersion=8.0`                   |
| `MYSQLDUMP_IGNORED_TABLES`                  | Contains a comma-separated list of tables which are to be ignored by the dump command. Asterisk can be used to specify several tables at once.          | `table1,table2,cache_*`                                                   |
| `MYSQLDUMP_FILTERED_TABLES`                 | Used to filter the content of tables. As an example only export data that is not deleted or is hidden (`deleted = 0 AND hidden = 0`).                   | `table3:"deleted = 0 AND hidden = 0",table4:"deleted = 0 AND hidden = 0"` |
| `$MYSQLDUMP_FILTERED_TABLES_DELETED_HIDDEN` | A shortcut for `MYSQLDUMP_FILTERED_TABLES` with `--where="deleted = 0 AND hidden = 0"`. Contains a comma-separated list of tables to be filtered.       | `table3,table4`                                                           |
| `MYSQLDUMP_TABLES_NO_DATA`                  | Contains a comma-separated list of tables from which no data should be dumped. Asterisk can be used to specify several tables at once.                  | `table5,table6_*`                                                         |
| `MYSQLDUMP_TABLES_ONLY_DATA`                | Contains a comma-separated list of tables from which no structure of tables should be dumped. Asterisk can be used to specify several tables at once.   | `table7,table8_*`                                                         |
| `MYSQLDUMP_VIEWS`                           | Contains a comma-separated list of views. Views will be imported after the tables are imported. Asterisk can be used to specify several tables at once. | `view1,view2_*`                                                           |

## Dump tables into db fixtures

### Via composer

```bash
vendor/bin/db-dumper dump
```

### Cloned project

```bash
bin/db-dumper dump
```

All dumps are then located in `./fixtures/db/*.sql`.

## Import existing db fixtures located in `./fixtures/db/*.sql` into database

### Via composer

```bash
vendor/bin/db-dumper import
```

### Cloned project

```bash
bin/db-dumper import
```

## Show help

Shows the parameters and arguments of the tool.

```bash
vendor/bin/db-dumper -h
```

```bash
db-dumper 0.1.1 (2023-28-01 18:07:16) - Björn Hempel <bjoern@hempel.li>

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

### Via composer

```bash
vendor/bin/db-dumper dump -d
```

```bash
vendor/bin/db-dumper import -d
```

### Cloned project

```bash
bin/db-dumper dump -d
```

```bash
bin/db-dumper import -d
```

## Show last log

```bash
vendor/bin/db-dumper -l
```

## Update version

```bash
vendor/bin/version-manager --patch
```

```bash
bin/db-dumper -u
```

```bash
rm bin/db-dumper && mv bin/db-dumper.tmp bin/db-dumper
```

```bash
vi CHANGELOG.md
```

## License

This tool is licensed under the MIT License - see the [LICENSE.md](/LICENSE.md) file for details
