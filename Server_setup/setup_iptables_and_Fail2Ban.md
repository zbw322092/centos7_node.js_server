# Setup iptables and Fail2Ban

## iptables vs firewalld
The relationship between iptables and firewalld.
> FirewallD is frontend controller for iptables used to implement persistent network traffic rules.

Differences:
> 1. FirewallD uses zones and services instead of chain and rules. 
>2. It manages rulesets dynamically, allowing updates without breaking existing sessions and connections.

>FirewallD is a wrapper for iptables to allow easier management of iptables rules–it is **not an iptables replacement**.


References about firewalld and iptables:
[1] https://www.linode.com/docs/security/firewalls/introduction-to-firewalld-on-centos<br/>

[2] https://www.linode.com/docs/networking/firewalls/control-network-traffic-with-iptables