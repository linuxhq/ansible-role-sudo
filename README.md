# ansible-role-sudo

[![Build Status](https://travis-ci.org/linuxhq/ansible-role-sudo.svg?branch=master)](https://travis-ci.org/linuxhq/ansible-role-sudo)

RHEL/CentOS - Execute a command as another user

## Requirements

None

## Role Variables

Available variables are listed below, along with default values:

    sudo_includedir: /etc/sudoers.d
    sudo_requiretty: True
    sudo_secure_path: [ '/sbin', '/bin', '/usr/sbin', '/usr/bin' ]
    sudo_visiblepw: False
    sudoers_d: []

You can define individual sudoers.d files using the following variable:

    sudoers_d:
      - file: tkimball
        user: tkimball
        commands:
          - /bin/su *

Additional variables available, not set by default:

    sudo_env_keep: [ 'GECOS', 'SSH_AUTH_SOCK' ]
    sudo_cmnd_alias:
      SERVICES: [ '/sbin/service', '/sbin/chkconfig' ]
    sudo_host_alias:
      FILESERVERS: [ 'fs1', 'fs2' ]
      MAILSERVERS: [ 'smtp', 'smtp2' ]
    sudo_user_alias:
      ADMINS: [ 'jsmith', 'mikem' ]
    sudo_wheel_nopasswd: False

## Dependencies

None

## Example Playbook

    - hosts: servers
      roles:
        - role: linuxhq.sudo
          sudo_env_keep: [ 'SSH_AUTH_SOCK' ]
          sudo_cmnd_alias:
            ansible: [ '/usr/bin/ansible', '/usr/bin/ansible-playbook' ]
          sudo_wheel_nopasswd: True
          sudoers_d:
            - file: tkimball
              user: tkimball
              commands:
                - /bin/su *

## License

BSD

## Author Information

This role was created by [Taylor Kimball](http://www.linuxhq.org).
