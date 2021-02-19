# mysqlshdump

mysqlshdump is a mysqlsh wrapper to run mysqldump commands using mysqlsh with the same parameters than mysqldump

While `mysqldump` has been the main tool to create logical backups of MySQL since many year, now [mysqlsh](https://dev.mysql.com/doc/mysql-shell/8.0/en/mysqlsh.html) is a [better tool in terms of performance](https://mysqlserverteam.com/mysql-shell-dump-load-part-2-benchmarks/). 

With this wrapper we can keep working mysqldump commands like: 

> mysqldump -h127.0.0.1 -uuser -ppass --databases db > file.sql

wrapped to be launched with mysqlsh:

> mysqlsh -h127.0.0.1 -uuser -ppass --py -e 'util.dump_schemas("db","/folder")'

The only changes you have to make are:

* Change the main command from `mysqldump` to `mysqlshdump`

* Change the bash redirection to a file by an [empty folder where mysqlsh will dump the files](https://dev.mysql.com/doc/mysql-shell/8.0/en/mysql-shell-utilities-dump-instance-schema.html). If that folder does not exist or is not empty, a new folder name with a timestamp will be used.

So you have to change this line:

> mysqldump -h127.0.0.1 -uuser -ppass --databases db > file.sql

by

> mysqlshdump -h127.0.0.1 -uuser -ppass --database db folder 

## Useful links:

* [MySQL Shell dumps](https://dev.mysql.com/doc/mysql-shell/8.0/en/mysql-shell-utilities-dump-instance-schema.html)
* [MySQL Shell CLI options](https://dev.mysql.com/doc/mysql-shell/8.0/en/mysqlsh.html)
* [mysqldump CLI options](https://dev.mysql.com/doc/refman/8.0/en/mysqldump.html#mysqldump-option-summary)


## TODO

* Implement `--triggers` and `--routines` options
