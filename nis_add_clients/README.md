nis_add_clients
=========

The Role is responsible for configuring a Linux client to be NIS client by installing the needed package for it (different of the Linux OS version) and adding the required parameters to the config files.
A part of the role is to replace DNS and NTP records to the ones which were added to role's dictionary.
Role is taking the information about location of IP (client) from Vault and linking this client to a closest NIS, DNS, NTP servers.

By default, the role is using

For Linux OS:

  - Vault authorization using microservice and its API endpoint
  - Local repository used for installing the needed packages and track the dependencies (for RHEL 6,7,8 and SLES 12 for now)

To use Hashicorp Vault we use API endpoint and the following code to query the credentials:

- name: Perform API call to endpoint
  uri:
    url: "{{ api_url }}"
    method: GET
    headers:
      Vault-Token: "{{ vault_token }}"
      Content-Type: "application/json"
    status_code: 200
    validate_certs: no
  delegate_to: localhost


Requirements
------------

Python 2.* for Linux operating system

Tested on:
  - RHEL 6.7; 6.8
  - CentOS 6.7; 7.2
  - SLES 11 SP4; 12
  - Ubuntu 14.04; 16.04, 18.04

Role Variables
--------------
Default variables:
- ansible_user - Administrator username
- ansible_password - Password
- os_is_windows: false
- os_is_linux: false
- os_is_esxi: false
- os_supported: false
- trimmed_os_pretty_name: "{{ os_name.stdout_lines[0] }}"
- centos: false
- rhel: false
- ubuntu: false
- suse: false
- other_os: false
- ubuntu_os: false
- nis_client_package_installed: false
- nis_client_running: false


Example Playbook
----------------

---
- name: nis_add_clients role
  hosts: all
  gather_facts: no
  vars:
  roles:
    - nis_add_clients