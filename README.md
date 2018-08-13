## Description

Ansible role to automate backups, using duplicity and duply for linux systems.
Tested in debian-like systems.

## features
- Make backups of files, full or incremental, with compression and encryption.
- Supports all storages that supports duplicity
- Make a dump of mysql, postgres or mongo and backed it as another file
- Creates a snapshot of a LXD container, promote it to image and export it to
tarball for backup it later. Leaves the last snapshot/image in the registry.

## Usage

Assign the role into your playbook, and define duply profiles in vars or inventory
Through the profiles you can config source files, destination, fulls and frecuency (cron execution)

## Variables

```
backup:
  remove: no
  cron: yes
  user: root
  group: root
  home: /etc/duply
  work: /var/duply
  logdir: /var/log/duply
  logrotate: yes

### default values, can be overrided in profiles
  gpg_key: disabled
  gpg_pw: ""
  gpg_opts: ''

  source: 'file:///etc'

  target: 'file:///var/backup'
  target_user: 'root'
  target_pass: 'root'


  max_age: 1Y
  max_full_backups: 8
  max_full_with_incr: 1
  full_max_age: 1W
  volsize: 50
  verbosity: 3
  exclude: []

postgres:
  postgres_user: postgres
  postgres_host: ""
  postgres_port: 5432

mysql:
  mysql_user: root
  mysql_pass: root



profiles:
### overrride default keys

# Ex. profiles:
#     - name: www
#       schedule: 0 0 * * 0
#       source: /var/www
#       max_age: 10D
#       target: s3://my.bucket/www
#       exclude:
#         - *.pyc
#     - name: postgresql
#       schedule: 0 4 * * *
#       action: restore
#       source: postgresql://db_name
#       target: s3://my.bucket/postgresql

- name: testjob
  schedule: "*/10 * * * *"  # remember quotes if use fractions.
  source: mysql://my
  target: file:///home/test/backups
  max_full_backups: 4
  full_max_age: 30m
  max_full_with_incr: 1
  mysql_user: root
  mysql_pass: root
```
## Dependencies

Ansible 2.5 or later

GPL v3 License
aizquierdo@mrmilu.com
