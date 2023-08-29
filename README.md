# [bareos_sd](#bareos_sd)

Install and configure [BareOS](https://www.bareos.com/) Storage Daemon on your system.

|GitHub|GitLab|Quality|Downloads|Version|
|------|------|-------|---------|-------|
|[![github](https://github.com/robertdebock/ansible-role-bareos_sd/workflows/Ansible%20Molecule/badge.svg)](https://github.com/robertdebock/ansible-role-bareos_sd/actions)|[![gitlab](https://gitlab.com/robertdebock-iac/ansible-role-bareos_sd/badges/master/pipeline.svg)](https://gitlab.com/robertdebock-iac/ansible-role-bareos_sd)|[![quality](https://img.shields.io/ansible/quality/63100)](https://galaxy.ansible.com/robertdebock/bareos_sd)|[![downloads](https://img.shields.io/ansible/role/d/63100)](https://galaxy.ansible.com/robertdebock/bareos_sd)|[![Version](https://img.shields.io/github/release/robertdebock/ansible-role-bareos_sd.svg)](https://github.com/robertdebock/ansible-role-bareos_sd/releases/)|

## [Example Playbook](#example-playbook)

This example is taken from [`molecule/default/converge.yml`](https://github.com/robertdebock/ansible-role-bareos_sd/blob/master/molecule/default/converge.yml) and is tested on each push, pull request and release.

```yaml
---
- name: Converge
  hosts: all
  become: yes
  gather_facts: no

  roles:
    - role: robertdebock.bareos_sd
      bareos_sd_directors:
        - name: dir-1
          password: "somepassword"
      bareos_sd_messages:
        - name: "Standard"
          description: "Send relevant messages to the Director."
          director:
            server: bareos-dir
            messages:
              - all
              - "!skipped"
              - "!restored"
          append:
            file: "/var/log/bareos/bareos.log"
            messages:
              - all
              - "!skipped"
              - "!terminate"
          console:
            - all
            - "!skipped"
            - "!saved"
      bareos_sd_devices:
        - name: "FileStorage"
          media_type: "File"
          archive_device: "/var/lib/bareos/storage"
          label_media: yes
          random_access: yes
          automatic_mount: yes
          removable_media: no
          always_open: no
          description: "File device. A connecting Director must have the same Name and MediaType."
```

The machine needs to be prepared. In CI this is done using [`molecule/default/prepare.yml`](https://github.com/robertdebock/ansible-role-bareos_sd/blob/master/molecule/default/prepare.yml):

```yaml
---
- name: Prepare
  hosts: all
  become: yes
  gather_facts: no

  roles:
    - role: robertdebock.bootstrap
    - role: robertdebock.bareos_repository
```

Also see a [full explanation and example](https://robertdebock.nl/how-to-use-these-roles.html) on how to use these roles.

## [Role Variables](#role-variables)

The default values for the variables are set in [`defaults/main.yml`](https://github.com/robertdebock/ansible-role-bareos_sd/blob/master/defaults/main.yml):

```yaml
---
# defaults file for bareos_sd

# The Storage Daemon has these configuration parameters.
bareos_sd_hostname: "{{ inventory_hostname }}"
bareos_sd_tls_enable: yes
bareos_sd_tls_verify_peer: no
```

## [Requirements](#requirements)

- pip packages listed in [requirements.txt](https://github.com/robertdebock/ansible-role-bareos_sd/blob/master/requirements.txt).

## [State of used roles](#state-of-used-roles)

The following roles are used to prepare a system. You can prepare your system in another way.

| Requirement | GitHub | GitLab |
|-------------|--------|--------|
|[robertdebock.bootstrap](https://galaxy.ansible.com/robertdebock/bootstrap)|[![Build Status GitHub](https://github.com/robertdebock/ansible-role-bootstrap/workflows/Ansible%20Molecule/badge.svg)](https://github.com/robertdebock/ansible-role-bootstrap/actions)|[![Build Status GitLab](https://gitlab.com/robertdebock-iac/ansible-role-bootstrap/badges/master/pipeline.svg)](https://gitlab.com/robertdebock-iac/ansible-role-bootstrap)|
|[robertdebock.bareos_repository](https://galaxy.ansible.com/robertdebock/bareos_repository)|[![Build Status GitHub](https://github.com/robertdebock/ansible-role-bareos_repository/workflows/Ansible%20Molecule/badge.svg)](https://github.com/robertdebock/ansible-role-bareos_repository/actions)|[![Build Status GitLab](https://gitlab.com/robertdebock-iac/ansible-role-bareos_repository/badges/master/pipeline.svg)](https://gitlab.com/robertdebock-iac/ansible-role-bareos_repository)|

## [Context](#context)

This role is a part of many compatible roles. Have a look at [the documentation of these roles](https://robertdebock.nl/) for further information.

Here is an overview of related roles:
![dependencies](https://raw.githubusercontent.com/robertdebock/ansible-role-bareos_sd/png/requirements.png "Dependencies")

## [Compatibility](#compatibility)

This role has been tested on these [container images](https://hub.docker.com/u/robertdebock):

|container|tags|
|---------|----|
|[Debian](https://hub.docker.com/repository/docker/robertdebock/debian/general)|all|
|[EL](https://hub.docker.com/repository/docker/robertdebock/enterpriselinux/general)|8, 9|
|[Fedora](https://hub.docker.com/repository/docker/robertdebock/fedora/general)|37|
|[opensuse](https://hub.docker.com/repository/docker/robertdebock/opensuse/general)|all|
|[Ubuntu](https://hub.docker.com/repository/docker/robertdebock/ubuntu/general)|jammy|

The minimum version of Ansible required is 2.12, tests have been done to:

- The previous version.
- The current version.
- The development version.

If you find issues, please register them in [GitHub](https://github.com/robertdebock/ansible-role-bareos_sd/issues)

## [License](#license)

[Apache-2.0](https://github.com/robertdebock/ansible-role-bareos_sd/blob/master/LICENSE).

## [Author Information](#author-information)

[robertdebock](https://robertdebock.nl/)

Please consider [sponsoring me](https://github.com/sponsors/robertdebock).
