oVirt Datacenters
=================

The `oVirt.datacenters` role is used to set up or cleanup oVirt datacenters.

n the special case of cleaning up oVirt datacenter that contains a Hosted Engine VM
the behavior of the role is different and is explained in more details in:
[ovirt-datacenter-cleanup]: https://github.com/oVirt/ovirt-ansible/blob/master/roles/ovirt-datacenter-cleanup/README.md

Requirements
------------

 * oVirt Python SDK version 4
 * Ansible version 2.4
 ( Ansible version 2.5 is required in case of using recursive_cleanup)

Role Variables
--------------

| Name                     | Default value         | Description                          |
|--------------------------|-----------------------|--------------------------------------|
| data_center_name         | UNDEF                 | Name of the data center.              |
| data_center_description  | UNDEF                 | Description of the data center.       |
| data_center_local        | false                 | Specify whether the data center is shared or local. |
| compatibility_version    | UNDEF                 | Compatibility version of data center. |
| data_center_state        | present               | Specify whether the datacenter should be present or absent. |
| recursive_cleanup        | false                 | Specify whether to recursively remove all entities inside DC. Valid only when I(state) == I(absent). |
| format_storages          | false                 | Specify whether to format ALL the storages that are going to be removed as part of the DC. Valid only when I(data_center_state) == I(absent) and I(recursive_cleanup) == I(true). |
| hosted_engine_vm_name    | HostedEngine          | Name of the hosted engine VM. If VM with such name exists HE environment is assumed. Valid only when I(data_center_state) == I(absent) and I(recursive_cleanup) == I(true). |

Dependencies
------------

None


Example Playbooks
----------------

```yaml
# Example 1

- name: Add oVirt datacenter
  hosts: localhost
  connection: local
  gather_facts: false

  vars:
   data_center_name: mydatacenter
   data_center_description: mydatacenter
   data_center_local: false
   compatibility_version: 4.1

  roles:
    - oVirt.infra/roles/oVirt.datacenters
```

```yaml
# Example 2

- name: Recursively remove oVirt datacenter
  hosts: localhost
  connection: local
  gather_facts: false

  vars:
   data_center_name: mydatacenter
   data_center_state: absent
   recursive_cleanup: true
   format_storages: true

  roles:
    - oVirt.infra/roles/oVirt.datacenters
```

License
-------

Apache License 2.0
