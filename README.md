# ansible-role-sudo

[![Build Status](https://travis-ci.org/linuxhq/ansible-role-sudo.svg?branch=master)](https://travis-ci.org/linuxhq/ansible-role-sudo)

RHEL/CentOS - Execute a command as another user

## Requirements

None

## Role Variables

Available variables are listed below, along with default values:

    sudoers_cmnd_aliases: {}
    sudoers_d: []
    sudoers_defaults:
      always_set_home: True
      env_reset: True
      match_group_by_gid: True
      requiretty: True
      secure_path: "/sbin:/bin:/usr/sbin:/usr/bin"
      visiblepw: False
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
              host: all
              runas: all
              user: tkimball
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

GPLv3

## Author Information

This role was created by [Taylor Kimball](http://www.linuxhq.org).
