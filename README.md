![Ansible Lint](https://github.com/johanneskastl/ansible-role-grafana_server/workflows/Ansible%20Lint/badge.svg)

grafana_server
=========

Install, configure and start a Grafana instance

Requirements
------------

None.

Role Variables
--------------

**Default values**

- `systemd_unit_name`: name of the systemd unit for the grafana server, defaults to `grafana-server.service`
- `grafana_system_user`: name of the system user for grafana, defaults to `grafana`
- `grafana_system_group`: name of the system group for grafana, defaults to `grafana`

**Role behaviour**

- `write_grafana_ini`: Boolean that decides if this roles writes the `grafana.ini` configuration file (default: `true`)
- `write_ldap_toml`: Boolean that decides if this roles writes the `ldap.toml` configuration file (default: `true`)

**TLS settings**

- `enable_tls`: Boolean that decides if TLS/ HTTPS should be enabled (Default: `false`)

If TLS is to be enabled, you need to set the following variables:

- `tls_certificate_crt_path`: path to the TLS certificate's crt file
- `tls_certificate_key_path`: path to the TLS certificate's key file

**LDAP settings**

- `enable_ldap`: Boolean that decides if LDAP authentication should be enabled (Default: `false`)

Dependencies
------------

None

Example Playbook
----------------

    - hosts: servers
      roles:
        - role: 'johanneskastl.grafana_server'

License
-------

BSD-3-Clause

Author Information
------------------

I am Johannes Kastl, reachable via kastl@b1-systems.de.
