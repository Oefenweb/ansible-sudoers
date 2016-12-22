## sudoers

[![Build Status](https://travis-ci.org/Oefenweb/ansible-sudoers.svg?branch=master)](https://travis-ci.org/Oefenweb/ansible-sudoers) [![Ansible Galaxy](http://img.shields.io/badge/ansible--galaxy-sudoers-blue.svg)](https://galaxy.ansible.com/tersmitten/sudoers)

Manage sudoers and sudoers.d in Debian-like systems.

#### Requirements

None

#### Variables

* `sudoers_sudoers`: `/etc/sudoers` file declarations
* `sudoers_sudoers.defaults`: [default: see `defaults/main.yml`]: Default configuration options
* `sudoers_sudoers.host_aliases`: [default: `[]`]: A list of aliases of type `Host_Alias`
* `sudoers_sudoers.host_aliases.name`: Name of the alias
* `sudoers_sudoers.host_aliases.members`: Member(s) of the alias
* `sudoers_sudoers.user_aliases`: [default: `[]`]: A list of aliases of type `User_Alias`
* `sudoers_sudoers.user_aliases.name`: Name of the alias
* `sudoers_sudoers.user_aliases.members`: Member(s) of the alias
* `sudoers_sudoers.cmnd_aliases`: [default: `[]`]: A list of aliases of type `Cmnd_Alias`
* `sudoers_sudoers.cmnd_aliases.name`: Name of the alias
* `sudoers_sudoers.cmnd_aliases.members`: Member(s) of the alias
* `sudoers_sudoers.runas_aliases`: [default: `[]`]: A list of aliases of type `Runas_Alias`
* `sudoers_sudoers.runas_aliases.name`: Name of the alias
* `sudoers_sudoers.runas_aliases.members`: Member(s) of the alias
* `sudoers_sudoers.privileges`: [default: see `defaults/main.yml`]: List of privileges
* `sudoers_sudoers.privileges.name`: Name of user or group (group should be prefixed with '%')
* `sudoers_sudoers.privileges.entry`: A privilege entry

* `sudoers_sudoers_d_files` [default: `{}`]: `/etc/sudoers.d/*` file(s) declarations
* `sudoers_sudoers_d_files.key`: The name of the sudoers configuration file (e.g `vagrant`)
* `sudoers_sudoers_d_files.key.defaults` [default: `[]`]: Default configuration options
* `sudoers_sudoers_d_files.key.host_aliases` [default: `[]`]: A list of aliases of type `Host_Alias`
* `sudoers_sudoers_d_files.key.host_aliases.name`: Name of the alias
* `sudoers_sudoers_d_files.key.host_aliases.members`: Member(s) of the alias
* `sudoers_sudoers_d_files.key.user_aliases` [default: `[]`]: A list of aliases of type `User_Alias`
* `sudoers_sudoers_d_files.key.user_aliases.name`: Name of the alias
* `sudoers_sudoers_d_files.key.user_aliases.members`: Member(s) of the alias
* `sudoers_sudoers_d_files.key.cmnd_aliases` [default: `[]`]: A list of aliases of type `Cmnd_Alias`
* `sudoers_sudoers_d_files.key.cmnd_aliases.name`: Name of the alias
* `sudoers_sudoers_d_files.key.cmnd_aliases.members`: Member(s) of the alias
* `sudoers_sudoers_d_files.key.runas_aliases` [default: `[]`]: A list of aliases of type `Runas_Alias`
* `sudoers_sudoers_d_files.key.runas_aliases.name`: Name of the alias
* `sudoers_sudoers_d_files.key.runas_aliases.members`: Member(s) of the alias
* `sudoers_sudoers_d_files.key.privileges` [default: `[]`]: List of privileges
* `sudoers_sudoers_d_files.key.privileges.name`: Name of user or group (group should be prefixed with '%')
* `sudoers_sudoers_d_files.key.privileges.entry`: A privilege entry

## Dependencies

None

#### Example(s)

##### Simple configuration

```yaml
---
- hosts: all
  roles:
    - sudoers
```

##### Complex configuration

```yaml
---
- hosts: all
  roles:
    - sudoers
  vars:
    sudoers_sudoers:
      defaults:
        - env_reset
        - exempt_group=sudo
        - mail_badpass
        - secure_path="/usr/local/sbin:/usr/local/bin:/usr/sbin:/usr/bin:/sbin:/bin"
      host_aliases:
        - name: CUNETS
          members: 128.138.0.0/255.255.0.0
        - name: SERVERS
          members: master, mail, www, ns
      user_aliases:
        - name: FULLTIMERS
          members: millert, mikef, dowdy
        - name: PARTTIMERS
          members: bostley, jwfox, crawl
      cmnd_aliases:
        - name: KILL
          members: /usr/bin/kill
        - name: HALT
          members: /usr/sbin/halt
      privileges:
        - name: root
          entry: "ALL=(ALL:ALL) ALL"
        - name: "%admin"
          entry: "ALL=(ALL) ALL"
        - name: "%sudo"
          entry: "ALL=NOPASSWD:ALL"
    sudoers_sudoers_d_files:
      test:
        defaults:
          - env_reset
          - exempt_group=sudo
          - mail_badpass
          - secure_path="/usr/local/sbin:/usr/local/bin:/usr/sbin:/usr/bin:/sbin:/bin"
        host_aliases:
          - name: WORKSTATIONS
            members: 128.138.0.0/255.255.0.0
        privileges:
          - name: test
            entry: "ALL=(ALL:ALL) ALL"    
```

#### License

MIT

#### Author Information

* Mark van Driel
* Mischa ter Smitten

#### Feedback, bug-reports, requests, ...

Are [welcome](https://github.com/Oefenweb/ansible-sudoers/issues)!
