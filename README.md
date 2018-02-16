Run VMWare esxi for local development such as testing terraform scripts.

username is root. password set vm startup

/etc/ssh/sshd_config needs to have PasswordAuthentication yes to allow ssh with password. There is no vagrant ssh setup on this box.

Set the IP and gateway (https://medium.com/@zedr/setting-up-the-vsphere-hypervisor-on-virtualbox-78d401bcd581). Network test is failing for DNS 8.8.8.8 and 4.4.4.4 servers. 

Requirements
------------

- Virtualbox 5.2+
- Vagrant 2.0.1+

Usage
-----

```
vagrant up
```

Author Information
------------------

Vang Nguyen

