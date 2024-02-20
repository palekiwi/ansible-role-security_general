Ansible Role: Server Security
=============================

Set up general security on a linux server, including user access, SSH settings, SELinux, firewall, fail2ban.

Requirements
------------

Requires EPEL repo to be enabled and the following ansible collections:

    collections:
      - ansible.posix
      - community.general

To install this role, in `requirements.yml` add:

    roles:
      - name: palekiwi.security_general
        src: http://github.com/palekiwi/ansible-role-security_general.git
        scm: git
        version: main

Run `ansible-galaxy install -r requirements.yml`.

Role Variables
--------------

Available variables and default values (see `defaults/main.yml`):

    # HELP create a user for ansible
    # TYPE string
    security_general_ansible_user: ansible

    # HELP ansible.posix.authorized_key
    # TYPE []{user: string, key: string}
    security_general_authorized_keys: []

    # HELP ansible.posix.sysctl
    # TYPE number | string
    security_general_ip_unpriviledged_port_start: 1024

    # HELP ssh port to listen on
    # TYPE number | string
    security_general_ssh_port: 22

    # HELP community.general.seport
    # TYPE []{ports: string | []string, proto: string, setype: string, state: string}
    security_general_selinux_ports: []

    # HELP ansible.posix.firewalld
    # TYPE []{state: string, port: string}
    security_general_firewalld_ports: []

    # HELP ansible.posix.firewalld
    # TYPE []{state: string, service: string}
    security_general_firewalld_services:
      - { state: "enabled", service: "http" }
      - { state: "enabled", service: "https" }
      - { state: "enabled", service: "ntp" }
      - { state: "enabled", service: "ssh" }
      - { state: "enabled", service: "dhcpv6-client" }
      - { state: "disabled", service: "cockpit" }

    # HELP ansible.posix.firewalld
    # TYPE string
    security_general_firewalld_zone: "public"

    # HELP configure automatic updates
    # TYPE bool
    security_general_automatic_updates: true

Dependencies
------------

None.

Example Playbook
----------------

Including an example of how to use your role (for instance, with variables passed in as parameters) is always nice for users too:

    - hosts: servers
      roles:
         - palekiwi.security_general

License
-------

BSD / MIT
