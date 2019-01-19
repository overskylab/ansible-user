Host preparation
=========

Ansible role to add ssh publickey into host.
- Configure authorized_keys

Requirements
------------

Before using this role. Please prepare your public key to be authorized_keys and configure ```user_authorized_keys_path``` to point to your authorized_keys files.

Role Variables
--------------

```yaml
# This is default variables
user_role_name: user

user_group_authorized_keys_path: "{{ playbook_dir }}/files/groups/{{ item }}/{{ user_role_name }}/authorized_keys"
user_group_authorized_keys_paths: []
user_global_authorized_keys_path: "{{ playbook_dir }}/files/authorized_keys"

user_put_authorized_keys_to_root: false
user_remove_password: true
user_remove_sudo_password: true
```

Dependencies
------------

NA

Example Playbook
----------------

Since Ubuntu Xenial did't come with python 2 by default. So playbook need to install python 2 first without gathering facts.

```yaml
- hosts: all
  gather_facts: no
  become: true
  pre_tasks:
    - name: Install Python 2 first
      raw: python --version || apt update && apt install -y python
  roles:
    - ansible-user
  vars_files:
    - "{{ user_vars_file }}"
```

List of useful tags
----------------

There are some useful tags that you can use to maintain your Ubuntu host.

- user-configure-authorized_keys
- user-configure

You can specific tag by using ```--tag``` for example if you only want to configure authorized_keys and limit to only production and database server group. You can run with command

License
-------

MIT
