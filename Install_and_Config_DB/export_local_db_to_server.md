# Export local database to server
First of all, [make `mysqldump` command accessable](https://stackoverflow.com/questions/38675885/how-to-make-mysql-dump-file-from-terminal-in-mac).
``` bash
export PATH=$PATH:/usr/local/mysql/bin
```
Or, you can access this command like this:
``` bash
/usr/local/mysql/bin/mysqldump -uroot -p friendstree > friendstree.sql
```
The dump file will locate at the directory which you execute above command.

After we generate dump file, we compress it using `tar` command.
```
tar cvzf MyTecBlogDump-2017-07-16.tar.gz MyTecBlogDump.sql
```
More on `tar` command: https://www.tecmint.com/18-tar-command-examples-in-linux/

How, we can upload compressed file to server using `scp` command.
For Example:
``` bash
$ scp -P 2344 myfile.txt root@example.com:/opt/myfile.txt
```
More on `scp`: https://b.oray.com/forward/


How, Decompressing `tar` file on server.
``` bash
sudo tar xvf MyTecBlogDump-2017-07-16.tar.gz
```

Execute `sql` file.
We get an uncompressed `sql` file now. We need to execute it. Taking follwing steps:
First of all, log in MySQL, and then create an database(since the sql file we created just contains tables create commands).
``` SQL
mysql> create database My_DB;

mysql> show databases;

mysql> use My_DB;
```
After creating a database, we execute `.sql` file in it. [Read It.](https://dev.mysql.com/doc/refman/5.7/en/mysql-batch-commands.html)
``` SQL
mysql> source file_name
```






Reference:<br/>
[1] https://www.howtogeek.com/howto/programming/mysql/dump-just-the-table-structure-to-a-file-in-mysql/<br/>
[2] https://dev.mysql.com/doc/refman/5.5/en/mysqldump-sql-format.html