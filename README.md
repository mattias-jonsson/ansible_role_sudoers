Ansible Role: ansible_role_sudoers
=========

An Ansible role that installs and configures sudo. The contents of the sudoers file is replaced with original content for each distribution and modifications will be added to the sudoers.d folder. Any modifications will result in a backup of original file, the name of the backup-file will be in the format of \<filename\>.{{timestamp}}.bkp.
This role supports the following Linux distributions:

<ul>
<li>CentOS 7/8
<li>Red Hat Enterprise Linux 7/8
<li>Ubuntu 18/20/22
</ul>

Requirements
------------

This role has no dependencies besides what is included in Ansible Core.

Role Variables
--------------

Available variables are listed below, along with default values where applicable (see defaults/main.yml):

    ansible_role_sudoersd_file:

This variable contains the name of the sudoers file which will be created under sudoers.d directory.


    ansible_role_sudoers_add_ansible_user: True

Boolean to select whether to add the ansible user to sudoers.d.

    ansible_role_sudoers_ansible_user_require_password: True

Boolean to select whether ansible user will be prompted for password for sudo operations.

    ansible_role_sudoers_cleanup: True

Boolean to select whether to cleanup any file in sudoers.d directory which is not created by this role. Any cleanedup file will be renamed with extension .disabled

    ansible_role_sudoers_cleanup_excludes:

List of filename to exclude from the cleanup operation.

    ansible_role_sudoers_dependencies:

Immutable variable from the vars folder containing a list of packages needed for this role.

    ansible_role_sudoersd_path: /etc/sudoers.d

Immutable variable from the vars folder containing path for sudoers.d files

    ansible_role_sudoers_file: /etc/sudoers

Immutable variable from the vars folder containing path of sudoers file

    name:

Configures sudoers target, this can be a user or group.

    require_password:

Require password for sudo operations.

    commands:

List of optional allowed sudo commands with or without arguments, NOEXEC will be added to each sudo command.


Dependencies
------------

This role has no external dependencies.

Example Playbook
----------------

Setup sudoers for someuser and someotheruser, also adds the ansible user to sudoers.d and sets it up to not require password for sudo operations.

    - hosts: servers

      vars:
        ansible_role_sudoers:
        - name: someuser
          require_password: true
          commands: 
            - /bin/something
            - /bin/something_else  -a1 -b2 -c3
        - name: someotheruser
          require_password: true
        ansible_role_sudoers_cleanup_excludes:
          - dont_disable_this_1
          - dont_disable_this_2
        ansible_role_sudoers_add_ansible_user: true
        ansible_role_sudoers_ansible_user_require_password: false
        ansible_role_sudoersd_file: 99_custom_sudoers

      roles:
         - role: ansible_role_sudoers

License
-------

MIT

Author Information
------------------

Mattias Jonsson