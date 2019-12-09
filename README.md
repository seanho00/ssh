# ho-ansible/ssh
Ansible role to configure ssh client/server

## Dependencies
+ ho-ansible.iptables

## Role variables
+ `ssh_port` (default: 22): TCP port server listens on
+ `ssh_whitelist` (default: all): allow (via firewall) only these
  hosts to connect to server.  Either IPv4 or IPv6 are ok.
+ `ssh_extra_cfg`: any extra lines to put in client config

## Regenerating host keys
This should be done by the openssh package already:
```
ssh-keygen -G /tmp/moduli-cand -b 4096
ssh-keygen -T /tmp/moduli -f /tmp/moduli-cand # slow!
mv /tmp/moduli /etc/ssh/moduli
rm /etc/ssh/ssh_host_*_key
ssh-keygen -t ed25519 -f /etc/ssh/ssh_host_ed25519_key
ssh-keygen -t rsa -b 4096 -f /etc/ssh/ssh_host_rsa_key
```

User keys:
```
ssh-keygen -t ed25519 -o -a 100
ssh-keygen -t rsa -b 4096 -o -a 100
```
