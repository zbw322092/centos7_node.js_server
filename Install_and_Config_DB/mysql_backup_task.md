# MySQL Backup Task

## create shell
To backup our database data, we can create a shell script and execute it regularly.
``` bash
#¡/bin/sh

backupFolder=/home/***/***/
date_now=`date +%Y_%m_%d_%H%M`
backupFileName=blog_$date_now

cd $backupFolder
mkdir -p $backupFileName

mysqldump -h 127.0.0.1:**** -u *** -p *** dbname > $backupFileName

tar zcvf $backupFileName.tar.gz $backupFileName

rm -rf $backupFileName
```

Get know more about `mysqldump` command:
https://stackoverflow.com/questions/13484667/downloading-mysql-dump-from-command-line<br/>
https://dev.mysql.com/doc/refman/5.7/en/mysqldump.html

More about `shell script`:
http://linuxcommand.org/writing_shell_scripts.php<br/>
https://stackoverflow.com/questions/1401482/yyyy-mm-dd-format-date-in-shell-script


## Set Regular Schedule
TODO