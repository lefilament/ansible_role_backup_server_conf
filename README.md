backup_server_conf
=========

This role is used to configure backup server for retrieving facts from all hosts via SFTP

Requirements
------------

None (all modules come from ansible.builtin collection)

Role Variables
--------------

This role makes use of the following group :
* backup_server : group listing all servers used for backup management

For all hosts that shoud be monitored, the following variable is expected (configured with init_server role) :
* backup_sftp_user : user to connect to backup servers with SFTP
* host_user_public_key : public key generated on each server to be used for SFTP connection

Variables from default directory :
swift parameters for 3 object storage (1 for cloud backups, 2 for Odoo backups) : these are used to list backups present in object storage for ensuring that backups are really performed daily

Variables from vars directory :
* python_apt_packages : list of packages for installing python3 and pip3
* swift_pip_packages : list of pip packages necessary for swift connection
* collect_backups : list of scripts to be pushed on backup servers to retrieve information about backup daily together with cron execution time


Dependencies
------------

This role depends on init_server role from Le Filament, since SSHD configuration file is retrieved from that role in order to maintain it in only one place.

Example Playbook
----------------

This role can be simply executed like follows (gathering facts is not necessary for this role)

        - hosts: backup_server
          gather_facts: false
          become: true
          roles:
          - { role: backup_server_conf, tags: backup }
          vars:
          - { swift_cloud_authurl: "https://auth.cloud.ovh.net/v3/" }
          - { swift_cloud_authversion: 3 }
          - { swift_cloud_tenantid: "12f1e" }
          - { swift_cloud_tenantname: "2214534534" }
          - { swift_cloud_username: "testuser" }
          - { swift_cloud_password: "testpassword" }
          - { swift_cloud_regionname: GRA }
          - { swift_odoo_authurl: "https://auth.cloud.ovh.net/v3/" }
          - { swift_odoo_authversion: 3 }
          - { swift_odoo_tenantid: "132e1fa" }
          - { swift_odoo_tenantname: "12312534534" }
          - { swift_odoo_username: "testuser" }
          - { swift_odoo_password: "testpassword" }
          - { swift_odoo_regionname: "GRA" }
          - { swift_odoo2_authurl: "https://auth.cloud.ovh.net/v3/" }
          - { swift_odoo2_authversion: 3 }
          - { swift_odoo2_tenantid: "12323534ab" }
          - { swift_odoo2_tenantname: "123124235345" }
          - { swift_odoo2_username: "testuser" }
          - { swift_odoo2_password: "testpassword" }
          - { swift_odoo2_regionname: "DE" }

License
-------

AGPL-3

Author Information
------------------

Le Filament (https://le-filament.com)
