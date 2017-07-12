# change server default port
``` bash
sudo vi /etc/ssh/sshd_config
```

change: 
``` bash
Port 8888
...
AllowUsers someone
```

Then restart this service:
In CentOS 7, we execute command like this may not success:
``` bash
$ service sshd restart
Redirecting to /bin/systemctl restart  sshd.service
==== AUTHENTICATING FOR org.freedesktop.systemd1.manage-units ===
Authentication is required to manage system services or units.
Authenticating as: ****
Password: 
==== AUTHENTICATION COMPLETE ===
Job for sshd.service failed because a configured resource limit was exceeded. See "systemctl status sshd.service" and "journalctl -xe" for details.
```

Here is the solution:<br/>
https://www.dropbit.ch/change-ssh-port-centos-7/<br/>
>Edit /etc/ssh/sshd_config and uncomment the port line to something like: “Port 4444”
Because CentOS 7 is a Security-Enhanced Linux (SELinux) you have to tell SELinux that running ssh on the new Port 4444 is allowed. This can be done by using the command “semanage”.
On a minimal CentOS 7 System the command “semanage” is missing therefore install it with “sudo yum install policycoreutils-python”
Afterwards you can use “semanage port -a -t ssh_port_t -p tcp 4444”, now SELinux allows sshd to listen on the new port 4444.
Check the configuration with “semanage port -l | grep ssh” and you should see something like:


more on this: <br/>
http://sharadchhetri.com/2014/10/15/centos-7-rhel-7-change-openssh-port-number-selinux-enabled/

Now, we change default port successfully. If we want to login like this, server will refuse you.
``` bash
ssh someone@192.168.1.1
ssh: connect to host 192.168.1.1 port 22: Connection refused
```

Solution(I forgot to add this rule):<br/>
https://serverfault.com/questions/667731/centos-7-firewalld-remove-direct-rule
``` bash
firewall-cmd --permanent --zone=public --add-port=12345/tcp

firewall-cmd --reload
```

During above operation, I added wrong port, the solution is remove the wrong port by follwing command:<br/>
https://www.linode.com/docs/security/firewalls/introduction-to-firewalld-on-centos
``` bash
sudo firewall-cmd --zone=public --remove-port=12345/tcp --permanent
```




Reference:
1. Connect to Linux from Mac OS X by using Terminal<br/>
https://support.rackspace.com/how-to/connecting-to-linux-from-mac-os-x-by-using-terminal/

2. AllowUsers<br/>
https://wiki.centos.org/HowTos/Network/SecuringSSH

3. ifconfig in centos 7
https://unix.stackexchange.com/questions/145447/ifconfig-command-not-found


