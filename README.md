ansible-role-postgresql
=========

Installation de postgresql


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
