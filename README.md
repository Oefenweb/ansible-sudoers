## sudoers

[![Build Status](https://travis-ci.org/Oefenweb/ansible-sudoers.svg?branch=master)](https://travis-ci.org/Oefenweb/ansible-sudoers) [![Ansible Galaxy](http://img.shields.io/badge/ansible--galaxy-sudoers-blue.svg)](https://galaxy.ansible.com/list#/roles/4827)

Manage sudoers in Debian-like systems.

#### Requirements

None

#### Variables

* `sudoers_sudoers`: sudoers configuration file declarations
* `sudoers_sudoers.defaults`: [default: see `defaults/main.yml`]
* `sudoers_sudoers.host_aliases`: [default: `[]`]:
* `sudoers_sudoers.host_aliases.alias`:
* `sudoers_sudoers.host_aliases.list`:
* `sudoers_sudoers.user_aliases`: [default: `[]`]:
* `sudoers_sudoers.user_aliases.alias`:
* `sudoers_sudoers.user_aliases.list`:
* `sudoers_sudoers.cmnd_aliases`: [default: `[]`]:
* `sudoers_sudoers.cmnd_aliases.alias`:
* `sudoers_sudoers.cmnd_aliases.list`:
* `sudoers_sudoers.runas_aliases`: [default: `[]`]:
* `sudoers_sudoers.runas_aliases.alias`:
* `sudoers_sudoers.runas_aliases.list`:
* `sudoers_sudoers.privileges`: [default: see `defaults/main.yml`]
* `sudoers_sudoers.privileges.name`: Name of user or group (group should be prefixed with '%').
* `sudoers_sudoers.privileges.entry`:
* `sudoers_sudoers_d_files` [default: `{}`]: sudoers configuration file declarations
* `sudoers_sudoers_d_files.key`: The name of the sudoers configuration file (e.g `vagrant`)
* `sudoers_sudoers_d_files.key.defaults` [default: `[]`]: 
* `sudoers_sudoers_d_files.key.host_aliases` [default: `[]`]:
* `sudoers_sudoers_d_files.key.host_aliases.alias`:
* `sudoers_sudoers_d_files.key.host_aliases.list`:
* `sudoers_sudoers_d_files.key.user_aliases` [default: `[]`]:
* `sudoers_sudoers_d_files.key.user_aliases.alias`:
* `sudoers_sudoers_d_files.key.user_aliases.list`:
* `sudoers_sudoers_d_files.key.cmnd_aliases` [default: `[]`]:
* `sudoers_sudoers_d_files.key.cmnd_aliases.alias`:
* `sudoers_sudoers_d_files.key.cmnd_aliases.list`:
* `sudoers_sudoers_d_files.key.runas_aliases` [default: `[]`]:
* `sudoers_sudoers_d_files.key.runas_aliases.alias`:
* `sudoers_sudoers_d_files.key.runas_aliases.list`:
* `sudoers_sudoers_d_files.key.privileges` [default: `[]`]:
* `sudoers_sudoers_d_files.key.privileges.name`: Name of user or group (group should be prefixed with '%').
* `sudoers_sudoers_d_files.key.privileges.entry`:

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
        - alias: CUNETS
          list: 128.138.0.0/255.255.0.0
        - alias: SERVERS
          list: master, mail, www, ns
      user_aliases:
        - alias: FULLTIMERS
          list: millert, mikef, dowdy
        - alias: PARTTIMERS
          list: bostley, jwfox, crawl
      cmnd_aliases:
        - alias: KILL
          list: /usr/bin/kill
        - alias: HALT
          list: /usr/sbin/halt
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
          - alias: WORKSTATIONS
            list: 128.138.0.0/255.255.0.0
        privileges:
          - name: test
            entry: "ALL=(ALL:ALL) ALL"    
```

#### License

MIT

#### Author Information

Mischa ter Smitten

#### Feedback, bug-reports, requests, ...

Are [welcome](https://github.com/Oefenweb/ansible-sudoers/issues)!
