# ansible-role-sudo

[![Build Status](https://travis-ci.org/linuxhq/ansible-role-sudo.svg?branch=master)](https://travis-ci.org/linuxhq/ansible-role-sudo)
[![Ansible Galaxy](https://img.shields.io/badge/ansible--galaxy-sudo-blue.svg?style=flat)](https://galaxy.ansible.com/linuxhq/sudo)
[![License](https://img.shields.io/badge/license-GPLv3-brightgreen.svg?style=flat)](COPYING)

RHEL/CentOS - Execute a command as another user

## Requirements

None

## Role Variables

Available variables are listed below, along with default values:

    sudoers_cmnd_aliases: {}
    sudoers_d: []
    sudoers_defaults:
      always_set_home: true
      env_reset: true
      match_group_by_gid: true
      requiretty: true
      secure_path: "/sbin:/bin:/usr/sbin:/usr/bin"
      visiblepw: false
    sudoers_host_aliases: {}
    sudoers_includedir: /etc/sudoers.d
    sudoers_privileges:
      - ugid: root
        host: ALL
        runas: ALL
        command: ALL
      - ugid: '%wheel'
        host: ALL
        runas: ALL
        command: ALL
    sudoers_runas_aliases: {}
    sudoers_user_aliases: {}

## Dependencies

None

## Example Playbook

    - hosts: servers
      roles:
        - role: linuxhq.sudo
          sudoers_cmnd_aliases:
            services:
              - /sbin/chkconfig
              - /sbin/service
          sudoers_d:
            - file: tkimball
              host: ALL
              runas: ALL
              ugid: tkimball
              commands:
                - 'certbot --renew'
                - 'systemctl restart ngircd.service'
          sudoers_host_aliases:
            fileservers:
              - fs1
              - fs2 
          sudoers_runas_aliases:
            appusers:
              - app1
              - app2
          sudoers_user_aliases:
            admins:
              - jsmith
              - mikem

## License

Copyright (C) 2018 Taylor Kimball <tkimball@linuxhq.org>

This program is free software: you can redistribute it and/or modify
it under the terms of the GNU General Public License as published by
the Free Software Foundation, either version 3 of the License, or
(at your option) any later version.

This program is distributed in the hope that it will be useful,
but WITHOUT ANY WARRANTY; without even the implied warranty of
MERCHANTABILITY or FITNESS FOR A PARTICULAR PURPOSE. See the
GNU General Public License for more details.

You should have received a copy of the GNU General Public License
along with this program. If not, see <http://www.gnu.org/licenses/>.
