Role Name
=========

Ansible role for setting up an xwiki instance that is powered by a docker stack. 

Requirements
------------

Docker must be installed on the orchestrated node, as well as `docker-compose`. 
This role defaults to `python3` for the `ansible-python-interpreter`. 
Python3 pip should be installed on the node so pip can install the python
dependencies necessary for this role.

Role variables
--------------

TODO: A description of the settable variables for this role should go here, including any variables that are in defaults/main.yml, vars/main.yml, and any variables that can/should be set via parameters to the role. Any variables that are read from other roles and/or the global scope (ie. hostvars, group vars, etc.) should be mentioned here as well.

Dependencies
------------

To install docker on the node [Jeff Geerling's ansible role for docker](
https://galaxy.ansible.com/geerlingguy/docker) is a recommended option.
Alternatively some linux distributions (such as Debian 10) offer docker in their repositories.

Example Playbook
----------------

TODO: Including an example of how to use your role (for instance, with variables passed in as parameters) is always nice for users too:

    - hosts: servers
      roles:
         - { role: username.rolename, x: 42 }

License
-------

MIT

Author Information
------------------

Ruben Vorderman, Leiden University Medical Center
