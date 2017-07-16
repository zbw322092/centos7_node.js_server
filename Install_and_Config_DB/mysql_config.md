# MySQL Configration
Start MySQL server
``` bash
sudo service mysqld start
```

Check MySQL status
``` bash
sudo service mysqld status
```

Check MySQL version
``` sql
SELECT VERSION();
```

MySQL configration file locates at `/etc/my.cnf`.
Set MySQL port like this:
``` bash
[mysqld]
datadir=/var/lib/mysql
socket=/var/lib/mysql/mysql.sock
port=****
```
And then restart service.
``` bash
sudo mysqld restart
```
You can check MySQL running port using following command:
``` bash
sudo netstat -tlnp
```
You will get similar result like this:
``` bash
tcp6       0      0 :::3306                :::*                    LISTEN      28425/mysqld
```

References:<br/>
[1] https://www.cyberciti.biz/faq/change-default-mysql-port-under-linuxunix/<br/>
[2] https://www.digitalocean.com/community/tutorials/how-to-install-mysql-5-6-from-official-yum-repositories<br/>
https://serverfault.com/questions/116100/how-to-check-what-port-mysql-is-running-on
