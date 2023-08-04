# Ansible Role: RabbitMQ

[![Test](https://github.com/ONLYOFFICE/ansible-role-rabbitmq/actions/workflows/ci.yml/badge.svg)](https://github.com/ONLYOFFICE/ansible-role-rabbitmq/actions/workflows/ci.yml)

Installs RabbitMQ on Linux.

## Role Variables

Available variables are listed below, along with default values (see [defaults/main.yml](defaults/main.yml)):

Controls the RabbitMQ daemon's state and whether it starts at boot.

    rabbitmq_daemon: rabbitmq-server
    rabbitmq_state: started
    rabbitmq_enabled: true

The Erlang and RabbitMQ versions to install.

    erlang_version: 25.3.2.4
    rabbitmq_version: 3.11.20

The Erlang and RabbitMQ versions to install on RedHat 7 / CentOS 7.

    erlang_version: 23.3.4.11
    rabbitmq_version: 3.10.0

## Dependencies

### community.rabbitmq

    ansible-galaxy collection install community.rabbitmq

## Example Playbook

    - hosts: all
      become: true

      pre_tasks:

        - name: Create dir for java
          file:
            path: /usr/share/man/man1
            state: directory

        - name: Update apt cache.
          apt: update_cache=yes force_apt_get=yes cache_valid_time=600
          when: ansible_os_family == 'Debian'

      roles:
        - onlyoffice.rabbitmq
