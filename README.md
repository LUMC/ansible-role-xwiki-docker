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
|xwiki_server_name (required)| localhost | the name of the server (for example:  xwiki.example.com). This is used in the nginx configuration.|
|xwiki_cfg| not set | `xwiki.cfg` file. When not set the container's default config will be used|
|xwiki_db_username| xwiki_db_user | The user for the xwiki database|
|xwiki_db_password (required) | not set | password for the xwiki database|
|xwiki_db_root_password (required) | not set | root password for the xwiki database|
|xwiki_docker_image_xwiki|xwiki:lts-postgres-tomcat|The docker image for xwiki. It is recommended to change this to a specific version.|
|xwiki_docker_image_postgres|postgres:latest|The docker image for postgres. It is recommended to change this to a specific version.|
|xwiki_docker_image_nginx|nginx:stable|The docker image for nginx. It is recommended to change this to a specific version.|
|xwiki_backup| true | By default a simple backup script is created that creates a tarball of the xwiki permanent directory and a sql backup of the xwiki database. This can be set to false if another backup solution is wanted.|
|xwiki_backup_log_dir| /var/lib/xwiki | where the backup log should be stored|
|xwiki_backup_script_dir| /var/lib/xwiki | where the backup script should be stored|
|xwiki_backup_dir| /var/lib/xwiki/backups| where the backups should be stored|
|xwiki_backup_max_age_days | 31 | The maximum age of backups (in days) before they are deleted |
|xwiki_backup_cron_minute| 0 | The backup script is run by cron. On this minute |
|xwiki_backup_cron_hour | 0 | |
|xwiki_backup_cron_day | * | |
|xwiki_backup_cron_weekday | 6 | By default one backup a week is made |
|xwiki_backup_cron_month | * | |
|xwiki_backup_remote_location | not set | if this is set, the backup script will rsync the `xwiki_backup_dir` to remote location. Examples: '/my_nfs_mount/xwiki_backups', 'backupuser@backup.example.com:/backups/xwiki'|
|xwiki_backup_ssh_key| not set | When the remote location is accessed through ssh, you can specify a private key file here that will be used for accessing it.|
|xwiki_backup_remote_host_name| not set | If remote location is accessed through ssh a remote host name is required (example: `backup.example.com`)|
|xwiki_backup_remote_host_public_key|not set| If remote location is accessed through ssh this is required. Can be acquired with `ssh-keyscan backup.example.com`. Takes the form of: `backup.example.com ssh-rsa AAAAB3etc.`|


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
