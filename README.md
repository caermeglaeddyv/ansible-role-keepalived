Ansible role: Keepalived
=========

This role is used to install keepalived by building it from source code.

For now, it does the following:
- downloads keepalived source files to localhost
- downloads build dependencies
- builds keepalived and configures it
- deletes build files and dependencies


Requirements
------------

This is not strict requirements and it may not work with other versions than tested ones.
Anyway. feel free to test by yourself, suggest addition of new functionality and contribute.

Role is tested with:
- Ansible version >= 2.8.6
- CentOS version >= 7.6 (1803)


Role Variables
--------------

Variables and their descriptions copied from defaults/main.yml

```bash

# Variable which is common for most projects, currently used
# to name VRRP instance inside configureation file:
keepalived_project_name: test

# Variable which is common for most projects, currently not used in this one:
keepalived_project_dir: files/{{ keepalived_project_name }}

# Keepalived source files version to download and build from:
keepalived_version: 2.0.19

# If keepalived is used with HAProxy which listens VRRP instance,
# enables checking if HAProxy process is alive or not:
keepalived_haproxy_check_script: false

# Virtual IP adddress which will fail over within cluster members:
keepalived_vip_address: ""

# Network interface for VRRP instance and to bind VIP on:
keepalived_vrrp_interface: "{{ ansible_default_ipv4.interface }}"

# Password to authentica between cluster members:
keepalived_auth_pass: "12345"

```


Dependencies
------------

none


Example Playbook
----------------

```bash
---
- hosts: localhost
  gather_facts: false
  become: no
  tasks:
  - name: Check ansible version >=2.8.6
    assert:
      msg: Ansible must be v2.8.6 or higher
      that:
      - ansible_version.string is version("2.8.6", ">=")
    tags:
    - check
  vars:
    ansible_connection: local

- hosts: all
  become: yes
  tasks:
  - import_role:
      name: keepalived

```

More detailed examples ( inventories, playbooks etc. ) of this and other roles can be found [here](https://github.com/caermeglaeddyv/examples/tree/dev/ansible).

It's highly recommended to start you test deploys from there, especially if you use Google Cloud Platform or VMware vCenter as your infrastructure, for now that [repository](https://github.com/caermeglaeddyv/examples) contains [Packer](https://github.com/caermeglaeddyv/examples/tree/dev/packer) and [Terraform](https://github.com/caermeglaeddyv/examples/tree/dev/terraform) examples to build templates and deploy machines on this platforms.


License
-------

[Apache 2.0](https://github.com/caermeglaeddyv/ansible-role-keepalived/blob/dev/LICENSE)


Author Information
------------------

Copyright 2020 [caermeglaeddyv](https://github.com/caermeglaeddyv)
