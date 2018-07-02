# ansible-role-yum_plugins

[![Build Status](https://travis-ci.org/linuxhq/ansible-role-yum_plugins.svg?branch=master)](https://travis-ci.org/linuxhq/ansible-role-yum_plugins)
[![Ansible Galaxy](https://img.shields.io/badge/ansible--galaxy-yum_plugins-blue.svg?style=flat)](https://galaxy.ansible.com/linuxhq/yum_plugins)
[![License](https://img.shields.io/badge/license-GPLv3-brightgreen.svg?style=flat)](COPYING)

RHEL/CentOS - Plug-ins that extend and enhance yums operations

## Requirements

None

## Role Variables

Available variables are listed below, along with default values:

    yum_plugin_fastestmirror: {}
    yum_plugin_post_transaction_actions: {}
    yum_plugin_pre_transaction_actions: {}

## Dependencies

None

## Example Playbook

    - hosts: servers
      roles:
        - role: linuxhq.yum_plugins
          yum_plugin_fastestmirror:
            always_print_best_host: true
            enabled: 1
            hostfilepath: timedhosts.txt
            maxhostfileage: 10
            maxthreads: 15
            socket_timeout: 3
            verbose: 0
          yum_plugin_post_transaction_actions:
            actiondir: /etc/yum/post-actions/
            actions:
              - action_key: kernel
                transaction_state: install
                command: /usr/sbin/grub2-set-default 0 && /usr/bin/systemctl reboot
            enabled: 1
          yum_plugin_pre_transaction_actions:
            actiondir: /etc/yum/pre-actions/
            actions:
              - action_key: httpd
                transaction_state: update
                command: /usr/bin/systemctl stop httpd.service
            enabled: 1

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

