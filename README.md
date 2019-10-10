# pg_check_update

pg_check_update is a script written in bash used to check if a postgres instance need update.

pg_check_update retrive version list from https://www.postgresql.org/support/versioning/ and check if your database is up to date.

If you are behind a proxy you have to set it before run pg_check_update. 

## Requirements

- Bash 4.0 or greater
- wget

## Actions

pg_check_update has the following actions:

```bash
[matteo@arch pg_check_update]$ ./pg_check_update --help
Usage:
   pg_check_update ACTION [OPTION] 

Actions:
  major     check if major version is available
  minor     check if minor version is available
  list      list all versions

  --help    display this help


Use pg_check_update ACTION --help to see specific action option
```

### major

Check if new major version is available for yuor database.

```bash
[mbona92@arch pg_check_update]$ ./pg_check_update major --help
Usage:
   pg_check_update major [OPTION]

Actions:
  -d        database to check (default: postgres)
  -h        database server host or socket directory (default: localhost)
  -p        database server port number (default: 5432)
  -U        connect as specified database user (default: postgres)

  --help    display this help

```
Example:

```bash
[mbona92@arch pg_check_update]$ ./pg_check_update major -d postgres -h pghost -p 5432 -U postgres
New major version(12) avaliable!
```

### minor

Check if new minor version (bug fix) is available for yuor database.

```bash
[mbona92@arch pg_check_update]$ ./pg_check_update minor --help
Usage:
   pg_check_update minor [OPTION]

Actions:
  -d        database to check (default: postgres)
  -h        database server host or socket directory (default: localhost)
  -p        database server port number (default: 5432)
  -U        connect as specified database user (default: postgres)

  --help    display this help

```

Example:

```bash
[mbona92@arch pg_check_update]$ ./pg_check_update minor -d postgres -h pghost -p 5432 -U postgres
New minor version (11.5) available!
```

### list

List all versions available.
It is possible to format output, for example, to load it in a database.

```bash
[mbona92@arch pg_check_update]$ ./pg_check_update list --help
Usage:
   pg_check_update list [OPTION]

Actions:
  --delimiter        specify delimiter within single quote
  --quote            quote all column
  --no-header        do not print header
  --supported        show only supported version

  --help    display this help
```

Examples:

```bash
[mbona92@arch pg_check_update]$ ./pg_check_update list
Version              Current_Minor        Supported            First_Release        Final_Release
12                   12.0                 Yes                  2019-10-03           2024-11-14
11                   11.5                 Yes                  2018-10-18           2023-11-09
10                   10.10                Yes                  2017-10-05           2022-11-10
9.6                  9.6.15               Yes                  2016-09-29           2021-11-11
9.5                  9.5.19               Yes                  2016-01-07           2021-02-11
9.4                  9.4.24               Yes                  2014-12-18           2020-02-13
9.3                  9.3.25               No                   2013-09-09           2018-11-08
9.2                  9.2.24               No                   2012-09-10           2017-11-09
9.1                  9.1.24               No                   2011-09-12           2016-10-27
9.0                  9.0.23               No                   2010-09-20           2015-10-08
8.4                  8.4.22               No                   2009-07-01           2014-07-24
8.3                  8.3.23               No                   2008-02-04           2013-02-07
8.2                  8.2.23               No                   2006-12-05           2011-12-05
8.1                  8.1.23               No                   2005-11-08           2010-11-08
8.0                  8.0.26               No                   2005-01-19           2010-10-01
7.4                  7.4.30               No                   2003-11-17           2010-10-01
7.3                  7.3.21               No                   2002-11-27           2007-11-27
7.2                  7.2.8                No                   2002-02-04           2007-02-04
7.1                  7.1.3                No                   2001-04-13           2006-04-13
7.0                  7.0.3                No                   2000-05-08           2005-05-08
6.5                  6.5.3                No                   1999-06-09           2004-06-09
6.4                  6.4.2                No                   1998-10-30           2003-10-30
6.3                  6.3.2                No                   1998-03-01           2003-03-01
```

```bash
[mbona92@arch pg_check_update]$ ./pg_check_update list --no-header --delimiter ';' --quote --supported
"12";"12.0";"Yes";"2019-10-03";"2024-11-14"
"11";"11.5";"Yes";"2018-10-18";"2023-11-09"
"10";"10.10";"Yes";"2017-10-05";"2022-11-10"
"9.6";"9.6.15";"Yes";"2016-09-29";"2021-11-11"
"9.5";"9.5.19";"Yes";"2016-01-07";"2021-02-11"
"9.4";"9.4.24";"Yes";"2014-12-18";"2020-02-13"
```

## out directory

pg_check_update save file downloaded from https://www.postgresql.org/support/versioning/ in out directory and make a cache file.

If new downloaded file is equal to the file downloaded in previuos run, pg_check_update use cache file instead of parse new file.

