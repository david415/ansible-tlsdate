Ansible tlsdate
===============

This is an Ansible role for use with tlsdate - https://github.com/ioerror/tlsdate

I hope that Tor relay, bridge and hidden service operators will find it useful.
Tor needs accurate time therefore I suggest using tlsdate rather than ntpd.


Requirements
------------

Works on Debian and Ubuntu.



Example Tor obfs4 Bridge Playbook using tlsdate
-----------------------------------------------

```yml
---
- hosts: tor-relays
  user: human
  connection: ssh
  roles:
    - { role: ansible-openssh-hardened,
        backports_url: "http://ftp.de.debian.org/debian/",
        backports_distribution_release: "wheezy-backports",
        ssh_admin_ed25519pubkey_path: "/home/amnesia/.ssh/id_ed25519.pub",
        sudo: yes
      }
    - { role: ansible-tlsdate,
        remove_ntp: yes,
        sudo: yes
      }
    - { role: ansible-tor,
        tor_distribution_release: "tor-experimental-0.2.5.x-wheezy",
        tor_BridgeRelay: 1,
        tor_PublishServerDescriptor: "bridge",
        tor_ExtORPort: "auto",
        tor_ORPort: 9001,
        tor_ServerTransportPlugin: "obfs4 exec /usr/bin/obfs4proxy",
        tor_ExitPolicy: "reject *:*",
        tor_obfs4proxy_enabled: True,
        sudo: yes
      }
```

License
-------

MIT


Feature requests and bug-reports welcome!
-----------------------------------------

https://github.com/david415/ansible-tlsdate/issues

