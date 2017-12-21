oVirt Datacenter Cleanup
========================

The `oVirt.datacenter-cleanup` role is used to cleanup all entities inside
oVirt datacenters and finally remove the datacenters themselves.

In the special case that the datacenter provided to cleanup contains a VM that
serves as Hosted Engine the role will not delete the following entities:

- the hosted engine VM itself.
- the storage domain on which the hosted engine VM resides.
- the master storage domain.
- the host and cluster which accommodate the hosted engine VM.
- the datacenter itself.


Requirements
------------

 * oVirt Python SDK version 4
 * Ansible version 2.4

Role Variables
--------------

| Name                     | Default value         | Description                          |
|--------------------------|-----------------------|--------------------------------------|
| data_center_name         | UNDEF                 | Name of the data center.             |
| format_storages          | false                 | Whether role should format storages when removing them. |
| hosted_engine_vm_name    | HostedEngine          | Name of the hosted engine VM. If VM with such name exists HE environment is assumed. |

Dependencies
------------

No.

Example Playbook
----------------

```yaml
- name: oVirt infra
  hosts: localhost
  connection: local
  gather_facts: false

  vars:
   data_center_name: mydatacenter
   format_storages: true

  roles:
    - oVirt.infra/roles/oVirt.datacenter-cleanup
```

License
-------

Apache License 2.0
