Ansible Role: ansible_role_sudoers
=========

Installs and configures sudo. The contents of the sudoers file is replaced with original content for each distribution and modifications will be added to the sudoers.d folder. Any modifications will result in a backup of original file. This role supports the following Linux distributions:

<ul>
<li>Enterprise Linux 7/8
<li>Ubuntu 18/20/22
</ul>

Requirements
------------

None.

Role Variables
--------------

| Variable | Required | Default | Comments |
| -------- | -------- | ------- | -------- |
| `ansible_role_sudoersd_file` | Yes | | This variable contains the name of the sudoers file which will be created under sudoers.d directory. |
| `ansible_role_sudoers_add_ansible_user` | No | True | Boolean to select whether to add the ansible user to sudoers.d. |
| `ansible_role_sudoers_ansible_user_require_password` | No | True | Boolean to select whether ansible user will be prompted for password for sudo operations. |
| `ansible_role_sudoers_cleanup` | No | True | Boolean to select whether to cleanup any file in sudoers.d directory which is not created by this role. Any cleanedup file will be renamed with extension .disabled |
| `ansible_role_sudoers_cleanup_excludes` | No | [] | List of filename to exclude from the cleanup operation. |
| `ansible_role_sudoers_file` | No | `defaults/main.yml` contains a list covering some versions  | A list of sha256 checksums for VMware Tools ISO files, format is version-build: sha256sum. Please verify and update this as needed. |
| `name` | Yes | | Configures sudoers target, this can be a user or group. |
| `require_password` | No | False | Require password for sudo operations. |
| `commands` | No | | List of optional allowed sudo commands with or without arguments, NOEXEC will be added to each sudo command. |

Dependencies
------------

None.

Example Playbook
----------------


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
