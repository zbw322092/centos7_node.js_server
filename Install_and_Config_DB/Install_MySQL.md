# Install MySQL
## Install
MySQL must be installed from the community repository.
``` bash
wget http://repo.mysql.com/mysql-community-release-el7-5.noarch.rpm

sudo rpm -ivh mysql-community-release-el7-5.noarch.rpm

yum update
```

Install MySQL as usual and start the service
``` bash
sudo yum install mysql-server
sudo systemctl start mysqld
```

## Security
Run the mysql_secure_installation script to address several security concerns in a default MySQL installation
``` bash
sudo mysql_secure_installation
```


Reference: <br/>
[1]https://www.linode.com/docs/databases/mysql/how-to-install-mysql-on-centos-7<br/>
[2] https://dev.mysql.com/downloads/repo/yum/