ovv.php7
========

[![Build Status](https://travis-ci.org/ovv/ansible-role-php7.svg?branch=master)](https://travis-ci.org/ovv/ansible-role-php7)

Ansible role to install and configure php-fpm pools.

Installation
------------

To install this roles clone it into your roles directory.

```bash
$ git clone https://github.com/ovv/ansible-role-php7.git ovv.php7
```

If your playbook already reside inside a git repository you can clone it by using git submodules.

```bash
$ git submodule add -b master https://github.com/ovv/ansible-role-php7.git ovv.php7
```

Role Variables
--------------

* `custom_php_packages`: Custom packages to install (default to empty).
* `php_pools`: Dict describing the php-fpm pools. Use the `key` as pool name.
    * `user`: Pool user (required).
    * `group`: Pool group (default to `user`).
    * `createhome`: Create home for `user` (default to `False`).
    * `home`: `user` home (default to `/home/{{ user }}`)
    * `working_dir`: Pool working directory (default to `/tmp`).
    * `socket`: PHP-fpm socket path (default to `/var/run/php7.0-fpm-{{ key }}.sock`)
    * `listen_owner`: Socket listen owner (default to `www-data`).
    * `listen_group`: Socket listen group (default to `www-data`).
    * `servers`: Servers to start (default to `2`).
    * `max_children` Maximum child servers (default to `5`).
    * `min_spare_servers`: Minimum spare servers (default to `1`).
    * `max_spare_servers`: Maximum spare servers (default to `3`).
* `base_php_packages`: Required packages to install (see [defaults](defaults/main.yml)).
* `php_memory_limit`: PHP memory limit (default to `128M`).
* `php_max_execution_time`: PHP max execution time (default to `300`).
* `php_smtp_host`: SMTP host (default to `localhost`).
* `php_smtp_port`: SMTP port (default to `25`).
* `php_sendmail_path`: Sendmail command (default to `/usr/sbin/sendmail -t -i`).


Example Playbook
----------------

```yml
- hosts: localhost
  vars:
    php_pools:
      example:
        user: example
  roles:
    - ansible-role-php7
```

License
-------

MIT
