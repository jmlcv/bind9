BIND9
=========

Ansible role install and configures ISC BIND and configures it in a way that VIEWS are Supported.
For more info on BIND Views, you may refer to https://kb.isc.org/article/AA-00851/0/Understanding-views-in-BIND-9-by-example.html

So far this role is only working for Ubuntu 14.04, but I intent to support more versions of this O.S., as well as other distros.

As of right now, this role will install and configure the BIND Name Server, but won't let you manage resource records. I plan to develop a new role for that. If you believe it would be helpfull, please let me know.

Please, feel free to let me know if you like it, and if you would like more stuff on this role.

Requirements
------------

Nothing specific so Far.
I have tested against Ubuntu 14.04, and ansible used was on version 1.93.


Role Variables
--------------

- bind9_installbind : (yes|no) Variable that controls whether the task to install Bind will be performed or skipped. In your group section on iventory file, you can use it to speed things up.
- bind9_confignamedconf : (yes|no) Variable that controls whether named.conf will be touched. You can skip it to improve performance.
- bind9_confignamedoptions : (yes|no) Variable that controls whether the Options file will be touched.
- bind9_confignamedacl : (yes|no) Variable that controls whether the ACLs file will be touched.
- bind9_confignamedviews : (yes|no) Variable that controls whether the list of dictionaries for BIND Views will be parsed. All files and directories required to organize zone data per view is handled.
- bind9_role : (master|slave) Variable that is used to control whether the server will be primary or secondary; For the example zone data, the 'type' section will say master, and for slave servers, 'type' will be slave and the masters directive is added. Also controls where zone data will be stored. By default, for master servers, it will be /etc/bind/view-$view_name/ and for slave servers, the directory will be /var/cache/bind/view-$view_name. Those directories are properly configure by default in APPARMOR



Dependencies
------------

None in particular so far.

Example Playbook
----------------

# Playbook example START

# Production DNS Servers
- hosts: prodservers
  remote_user: ubuntu
  sudo: yes
  roles:
    - { role: bind9, installbind: no }

# Development Servers
- hosts: devservers
  remote_user: ubuntu
  sudo: yes
  roles:
    - { role: bind9 }

# Playbook example STOP

Group Variables
---------------

# group prodservers Example START

---
BIND_VIEWS:
  # External View
  - { view_name: external, match_client_acl: "everybody;", recursion: "no", allow_recursion: "none;" }
  # Internal View
  - { view_name: internal, match_client_acl: "internal;", recursion: "yes", allow_recursion: "any;" }

# group prodservers Example STOP

License
-------

APACHE

Author Information
------------------

Jose Manuel Valente - jmlcv@yahoo.com
