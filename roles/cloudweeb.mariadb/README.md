Ansible Role Mariadb
=========

[![Build Status](https://travis-ci.com/cloudweeb/cloudweeb.mariadb.svg?branch=master)](https://travis-ci.com/cloudweeb/cloudweeb.mariadb)

Ansible role to install MariaDB server

Requirements
------------

None

Role Variables
--------------

```YAML
mariadb_version: 10.3   # MariaDB version that wants to be installed

mariadb_root_password: password

# MariaDB additional packages
mariadb_packages: []
# - MariaDB-devel
# - MariaDB-shared

# MariaDB network config
mariadb_skip_networking: false
mariadb_skip_name_resolve: false
mariadb_bind_address: '0.0.0.0'   # MariaDB listen address
mariadb_port: '3306'              # MariaDB listen port

mariadb_pid_file: /var/lib/mysql/{{ ansible_fqdn }}.pid

# MariaDB log config
mariadb_slow_query_log: false
mariadb_error_log_file: /var/lib/mysql/{{ ansible_fqdn }}.err
mariadb_slow_query_log_file: /var/lib/mysql/{{ ansible_fqdn }}.slow-query.log

# MariaDB resource config
mariadb_key_buffer_size: 16K
mariadb_max_allowed_packet: 1M
mariadb_table_open_cache: '2000'
mariadb_sort_buffer_size: 64K
mariadb_read_buffer_size: 256K
mariadb_read_rnd_buffer_size: 256K
mariadb_net_buffer_length: 2K
mariadb_thread_stack: 240K
mariadb_max_connections: '50'
mariadb_max_user_connections: '25'
mariadb_wait_timeout: '10'
mariadb_interactive_timeout: '50'
mariadb_long_query_time: '5'

# MariaDB innodb config
mariadb_innodb_file_per_table: true
mariadb_innodb_buffer_pool_size: 128M
mariadb_innodb_log_file_size: 48M
mariadb_innodb_buffer_pool_instances: '1'

mariadb_users: []
# - name: example
#   password: example
#   priv: "*.*:USAGE"
#   state: present

mariadb_databases: []
# - name: example
#   state: present
```

Dependencies
------------

None

Example Playbook
----------------

    - hosts: servers
      vars:
        mariadb_root_password: "{{ lookup('password', '/tmp/mariadb_root_password length=15 chars=ascii_letters,digits,hexdigits') }}"

        mariadb_users:
          - name: example
            password: "{{ lookup('password', '/tmp/mariadb_example_password length=15 chars=ascii_letters,digits,hexdigits') }}"
            priv: "example.*:ALL"
            state: present

        mariadb_databases:
          - name: example
            state: present

      roles:
        - role: cloudweeb.mariadb

License
-------

BSD/MIT

Author Information
------------------

Agnesius Santo Naibaho
