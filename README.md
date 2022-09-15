# Ansible Role: RabbitMQ
[![Test](https://github.com/ONLYOFFICE/ansible-role-rabbitmq/actions/workflows/ci.yml/badge.svg)](https://github.com/ONLYOFFICE/ansible-role-rabbitmq/actions/workflows/ci.yml)

Installs RabbitMQ on Linux.

## Role Variables

Available variables are listed below, along with default values (see `defaults/main.yml`):

    rabbitmq_daemon: rabbitmq-server
    rabbitmq_state: started
    rabbitmq_enabled: true

Controls the RabbitMQ daemon's state and whether it starts at boot.

    rabbitmq_version: "{{ '3.7.18' if ansible_distribution_release == 'buster' else '3.6.16' }}"

The RabbitMQ version to install.

    rabbitmq_focal_version: "3.8.8"
    
The RabbitMQ version to install for Ubuntu 20.04.

    rabbitmq_bullseye_version: "3.15.8"

The RabbitMQ version to install for Ubuntu 22.04.

    rabbitmq_bullseye_version: "3.8.33"

The RabbitMQ version to install for Debian Bullseye.

    rabbitmq_el8_version: "3.8.8"
    
The RabbitMQ version to install for Centos8.

    rabbitmq_rpm: "rabbitmq-server-{{ rabbitmq_version }}-1.el{{ ansible_distribution_major_version }}.noarch.rpm"
    rabbitmq_el8_rpm: "rabbitmq-server-{{ rabbitmq_el8_version }}-1.el{{ ansible_distribution_major_version }}.noarch.rpm"
    rabbitmq_rpm: "rabbitmq-server-{{ rabbitmq_version }}-1.el{{ ansible_distribution_major_version }}.noarch.rpm"
    rabbitmq_rpm_url: "https://packagecloud.io/rabbitmq/rabbitmq-server/packages/el/{{ ansible_distribution_major_version }}/{{ rabbitmq_rpm }}/download"
    rabbitmq_el8_rpm_url: "https://packagecloud.io/rabbitmq/rabbitmq-server/packages/el/{{ ansible_distribution_major_version }}/{{ rabbitmq_el8_rpm }}/download"
    rabbitmq_gpg_key: "https://packagecloud.io/rabbitmq/rabbitmq-server/gpgkey"

(RedHat/CentOS only) Controls the .rpm to install.

    rabbitmq_deb: "rabbitmq-server_{{ rabbitmq_version }}-1_all.deb"
    rabbitmq_focal_deb: "rabbitmq-server_{{ rabbitmq_focal_version }}-1_all.deb"
    rabbitmq_jammy_deb: "rabbitmq-server_{{ rabbitmq_jammy_version }}-1_all.deb"
    rabbitmq_bullseye_deb: "rabbitmq-server_{{ rabbitmq_bullseye_version }}-1_all.deb"
    rabbitmq_deb_url: "https://packagecloud.io/rabbitmq/rabbitmq-server/packages/{{ ansible_distribution | lower }}/{{ ansible_distribution_release }}/{{ rabbitmq_deb }}/download"
    rabbitmq_focal_deb_url: "https://packagecloud.io/rabbitmq/rabbitmq-server/packages/{{ ansible_distribution | lower }}/bionic/{{ rabbitmq_focal_deb }}/download"
    rabbitmq_jammy_deb_url: "https://packagecloud.io/rabbitmq/rabbitmq-server/packages/{{ ansible_distribution | lower }}/jammy/{{ rabbitmq_jammy_deb }}/download"
    rabbitmq_bullseye_deb_url: "https://packagecloud.io/rabbitmq/rabbitmq-server/packages/{{ ansible_distribution | lower }}/bullseye/{{ rabbitmq_bullseye_deb }}/download"

(Debian/Ubuntu only) Controls the .deb to install.

## Dependencies

None.

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
