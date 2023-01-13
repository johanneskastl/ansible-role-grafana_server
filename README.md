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

If LDAP is enable with the `enable_ldap` variable, then the following settings need to be made:

- `ldap_server_url`: LDAP server URL (without port)
- `ldap_server_port`: Port on the LDAP server (probably `389` or `636`, depending on your TLS settings)
- `ldap_bind_dn`: DN to bind to the LDAP server
- `ldap_bind_password`: Password for the bind DN
- `ldap_search_filter`: LDAP search filter to lookup the users
- `ldap_search_base_dns`: search base for the user lookup
- `ldap_admin_group_dn`: `group_dn` describing the `Admin` group
- `ldap_editors_group_dn`: `group_dn` describing the `Editors` group

The following variables can be set, if needed:

- `ldap_server_root_ca_cert_path`: CA certificate to validate the server's TLS certificate
- `ldap_server_client_certificate_crt_path`: crt file for the client certificate (for certificate-based authentication)
- `ldap_server_client_certificate_key_path`: key file for the client certificate (for certificate-based authentication)

The following variables can be set, if their default value does not fit your needs:

- `ldap_allow_sign_up`: If set to `'true'`, new users can log in via LDAP. If set to `'false'`, only previously logged in users can log in again (default: `'true'`)
- `path_to_ldap_toml`: path to the `ldap.toml` file, defaults to `/etc/grafana/ldap.toml`
- `ldap_server_use_ssl`: whether to use SSL (default: `false`)
- `ldap_server_start_tls`: whether to use StartTLS (default: `false`)
- `ldap_server_skip_ssl_verify`: whether to skip SSL verification  (default: `false`)
- `ldap_search_filter`: search filter for the user (default: `(cn=%s)`)
- `ldap_attributes_name`: LDAP attribute that contains the user's name (default: `givenName`)
- `ldap_attributes_surname`: LDAP attribute that contains the user's surname (default: `sn`)
- `ldap_attributes_username`: LDAP attribute that contains the user's username (default: `cn`)
- `ldap_attributes_memberof`: LDAP attribute for memberships (default: `memberOf`)
- `ldap_attributes_email`: LDAP attribute that contains the user's email address (default: `email`)
- `ldap_admin_group_make_grafana_admin`: whether to make the admin group grafana admins (default: `false`)
- `ldap_admin_group_org_id`: ID of the organization that the admin group is made admin of (default: `1`)
- `ldap_viewer_group_dn`: `group_dn` describing the `Viewer` group (default: `*`)

Dependencies
------------

None

Example Playbook
----------------

    - hosts: grafana-server01
      roles:
        - role: 'johanneskastl.grafana_server'

Example Playbook using TLS
----------------

    - hosts: grafana-server01
      roles:
        - role: 'johanneskastl.grafana_server'
          enable_tls: true
          tls_certificate_crt_path: '/etc/ssl/my_server.crt'
          tls_certificate_key_path: '/etc/ssl/my_server.key'

Example Playbook using LDAP and TLS)
----------------

    - hosts: grafana-server01
      roles:
        - role: 'johanneskastl.grafana_server'
          enable_tls: true
          tls_certificate_crt_path: '/etc/ssl/my_server.crt'
          tls_certificate_key_path: '/etc/ssl/my_server.key'
          enable_ldap: true
          ldap_server_url: ldap.example.org
          ldap_server_port: 389
          ldap_server_start_tls: 'true'
          ldap_bind_dn: 'johndoe'
          ldap_bind_password: 'super_secret' # should not be defined here, rather in a separate file encrypted with Ansible vault
          ldap_search_base_dns: 'dc=example,dc=org'
          ldap_admin_group_dn: 'cn=grafana_admins,ou=groups,dc=example,dc=org'
          ldap_editors_group_dn: 'cn=grafana_users,ou=groups,dc=example,dc=org'

License
-------

BSD-3-Clause

Author Information
------------------

I am Johannes Kastl, reachable via kastl@b1-systems.de.
