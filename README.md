# Automysqlbackup

[![Build Status](https://travis-ci.org/guisea/ansible-role-automysqlbackup.svg?branch=master)](https://travis-ci.org/guisea/ansible-role-automysqlbackup)

Installs and configures the automysqlbackup utility on RHEL/CentOS or Debian/Ubuntu servers.

## Requirements

No special requirements; note that this role requires root access, so either run it in a playbook with a global `become: yes`, or invoke the role in your playbook like:

    - hosts: mysql-database
      roles:
        - role: guisea.automysqlbackup
          become: yes


---

**Variables**

```
# database username and password that will perform the backups
automysqlbackup_username: "$(grep user /etc/mysql/debian.cnf | tail -n 1 | cut -d'=' -f2 | awk '{print $1}')"
automysqlbackup_password: "$(grep password /etc/mysql/debian.cnf | tail -n 1 | cut -d'=' -f2 | awk '{print $1}')"

# hostname or ip address of the database server
automysqlbackup_host: localhost

# space separated string of databases to include or ignore in the backup
automysqlbackup_dbames: "all"
automysqlbackup_dbexclude: ""

# whether to include a create database statement
automysqlbackup_createdb_stmt: "yes"

automysqlbackup_backup_directory: /var/lib/automysqlbackup

# backup each database in a separate directory or everything to a single file
automysqlbackup_sepdir: "yes"

# day of the week for weekly backbackups (6 - Saturday)
automysqlbackup_doweekly: 6

# output location (log, files, stdout, quiet) and where output is sent (user / email address)
automysqlbackup_mailcontent: quiet
automysqlbackup_mailaddr: root

# default cron configuration
automysqlbackup_cron:
  minute: 0
  hour: 0
  day: "*"
  month: "*"
  weekday: "*"

# latest
automysqlbackup_latest: "no"

```

## License

MIT

---