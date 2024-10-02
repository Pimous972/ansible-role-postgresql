ansible-role-postgresql
=========

Installation de postgresql

Requirements
------------

Any pre-requisites that may not be covered by Ansible itself or the role should be mentioned here. For instance, if the role uses the EC2 module, it may be a good idea to mention in this section that the boto package is required.

Role Variables
--------------

```yaml
# default/mail.yml or in inventories/group_vars/<group_name>.yml
postgresql_version: 15
postgresql_hba_entries:
  - { type: local, database: all, user: postgres, auth_method: peer }
  - { type: local, database: all, user: all, auth_method: peer }
  - { type: local, database: all, user: dba, auth_method: scram-sha-256 }
  - {
      type: host,
      database: all,
      user: dba,
      address: "{{ groups['admin'][0] }}/32",
      auth_method: scram-sha-256,
    }
  - {
      type: host,
      database: all,
      user: dba,
      address: "0.0.0.0/32",
      auth_method: scram-sha-256,
    }
```


Example Playbook
----------------
```yaml
- hosts: postgresql
  vars_files:
    - vault.yml
  roles:
    - ansible-role-postgresql
  tags: [postgresql]
```

License
-------

MIT

Author Information
------------------

pimoos972@gmail.com
