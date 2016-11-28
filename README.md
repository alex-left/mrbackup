## Description

Ansible role to automate backups, through duplicity and his frontend duply

## Usage

Assign the role into your playbook, and define duply profiles through variables

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

Ansible 2.2 or later

A short snippet describing the license (MIT, Apache, etc.)