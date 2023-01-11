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
- `grafana_system_group`: name of the system group for grafana, defaults to `grafana`

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
