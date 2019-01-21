# PowerDNS zabbix template

* Based on [powerdns-and-powerdns-recursor](https://share.zabbix.com/cat-app/powerdns-and-powerdns-recursor) by [Martin Mørch](https://share.zabbix.com/owner/g_117277102264138294427)

### Features

* Version reporting
* Security alerts

### PowerDNS auth

#### Installation

* [`/etc/sudoers.d/pdns-auth`](etc/sudoers.d/pdns-auth):

  ```
  # Zabbix Agent PDNS
  Defaults:zabbix !requiretty
  zabbix ALL=NOPASSWD: /usr/bin/pdns_control
  ```

* [`/etc/zabbix/zabbix_agentd.d/pdns-auth.conf`](etc/zabbix/zabbix_agentd.d/pdns-auth.conf):

  ```
  UserParameter=pdns_stats[*],/usr/bin/sudo /usr/bin/pdns_control show $1
  UserParameter=pdns_version,/usr/bin/sudo /usr/bin/pdns_control version
  ```

### PowerDNS recursor

#### Installation

* [`/etc/sudoers.d/pdns-rec`](etc/sudoers.d/pdns-rec):

  ```
  # Zabbix Agent PDNS Recursor
  Defaults:zabbix !requiretty
  zabbix ALL=NOPASSWD: /usr/bin/rec_control
  ```

* [`/etc/zabbix/zabbix_agentd.d/pdns-recursor.conf`](etc/zabbix/zabbix_agentd.d/pdns-recursor.conf):

  ```
  UserParameter=pdnsrec_stats[*],/usr/bin/sudo /usr/bin/rec_control get $1
  UserParameter=pdnsrec_version,/usr/bin/sudo /usr/bin/pdns_control version
  ```
