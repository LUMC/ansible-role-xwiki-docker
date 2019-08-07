Ansible role: xwiki-docker
==========================

Ansible role for setting up an xwiki instance that is powered by a docker stack.

Requirements
------------

Docker must be installed on the orchestrated node, as well as `docker-compose`.
This role defaults to `python3` for the `ansible-python-interpreter`.
Python3 pip should be installed on the node so pip can install the python
dependencies necessary for this role.

Role variables
--------------

|variable|default|description|
|--------|-------|-----------|
|ansible_python_interpreter| python3 |  This role only works with python3! You can set a specific python interpreter on the host with this variable|
|xwiki_server_key (required)| not set | The servers private key for enabling https|
|xwiki_server_cert (required)| not set | The servers certificate for https|
|xwiki_cfg| not set | `xwiki.cfg` file. When not set the container's default config will be used|
|xwiki_db_username| xwiki_db_user | The user for the xwiki database|
|xwiki_db_password (required) | not set | password for the xwiki database|
|xwiki_db_root_password (required) | not set | root password for the xwiki database|



TODO: A description of the settable variables for this role should go here, including any variables that are in defaults/main.yml, vars/main.yml, and any variables that can/should be set via parameters to the role. Any variables that are read from other roles and/or the global scope (ie. hostvars, group vars, etc.) should be mentioned here as well.

Dependencies
------------

To install docker on the node [Jeff Geerling's ansible role for docker](
https://galaxy.ansible.com/geerlingguy/docker) is a recommended option.
Alternatively some linux distributions (such as Debian 10) offer docker in their repositories.

Example Playbook
----------------

```YAML
- hosts: debian-10-xwiki
  pre_tasks:
    - name: Install docker prerequisites
      apt:
        name:
          - docker.io
          - docker-compose
          state: present

    - name: Install pip for python3
        apt:
          name: python3-pip
          state: present
  roles:
    - role: ansible-role-xwiki-docker
```

License
-------

MIT

Author Information
------------------

Ruben Vorderman, Leiden University Medical Center
