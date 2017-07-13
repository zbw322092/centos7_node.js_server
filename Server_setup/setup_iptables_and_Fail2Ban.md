# Setup iptables and Fail2Ban

## iptables vs firewalld
The relationship between iptables and firewalld.
> FirewallD is frontend controller for iptables used to implement persistent network traffic rules.

Differences:
> 1. FirewallD uses zones and services instead of chain and rules. 
>2. It manages rulesets dynamically, allowing updates without breaking existing sessions and connections.

>FirewallD is a wrapper for iptables to allow easier management of iptables rules–it is **not an iptables replacement**.


I use firewalld to coontroll network traffic in my server.
I modified configuration based on public zone.
> public: Represents public, untrusted networks. You don't trust other computers but may allow selected incoming connections on a case-by-case basis.

Configuration Example:(excerpt from [5])
``` bash
# allow http services permanently
sudo firewall-cmd --zone=public --permanent --add-service=http
``` 

Common Command in `firewalld`
``` bash
# start the daemon for this session
sudo systemctl start firewalld.service

#  verify that the service is running and reachable
firewall-cmd --state

# print out the default zone's configuration
firewall-cmd --list-all

# which zone is currently selected
firewall-cmd --get-default-zone

# active zone
firewall-cmd --get-active-zones

# get zones
firewall-cmd --get-zones

# get services
firewall-cmd --get-services

# add services
sudo firewall-cmd --zone=public --add-service=http

sudo firewall-cmd --zone=public --permanent --add-service=http

# add ports
sudo firewall-cmd --zone=public --permanent --add-port=5000/tcp

# restart firewall service
sudo systemctl restart firewalld.service
```

References about firewalld and iptables:
[1] https://www.linode.com/docs/security/firewalls/introduction-to-firewalld-on-centos<br/>

[2] https://www.linode.com/docs/networking/firewalls/control-network-traffic-with-iptables<br/>

[3] https://www.digitalocean.com/community/tutorials/how-to-migrate-from-firewalld-to-iptables-on-centos-7<br/>

[4] https://www.digitalocean.com/community/tutorials/iptables-essentials-common-firewall-rules-and-commands<br/>

[5] https://www.digitalocean.com/community/tutorials/how-to-set-up-a-firewall-using-firewalld-on-centos-7<br/>
[6] https://jpopelka.fedorapeople.org/firewalld/doc/firewalld.richlanguage.html<br/>
[7] https://fedoraproject.org/wiki/Features/FirewalldRichLanguage