# Ansible Role: repositories

[![Build Status](https://img.shields.io/travis/arillso/ansible.repositories.svg?branch=master&style=popout-square)](https://travis-ci.org/arillso/ansible.repositories) [![license](https://img.shields.io/github/license/mashape/apistatus.svg?style=popout-square)](https://sbaerlo.ch/licence) [![Ansible Galaxy](https://img.shields.io/badge/ansible--galaxy-repositories-blue.svg?style=popout-square)](https://galaxy.ansible.com/arillso/repositories) [![Ansible Role](https://img.shields.io/ansible/role/d/id.svg?style=popout-square)](https://galaxy.ansible.com/arillso/repositories)

## Description

Manages Repository under CentOS and Ubuntu. By default the epel Repository will be set up at CentOS and on Ubuntu Universe Repository.

## Installation

```bash
ansible-galaxy install arillso.repositories
```

## Requirements

None

## Role Variables

### repositories

Repositories is a list of repositories that should be added to a system, but they differ by the key `Ubuntu` or `CentOS`.

#### ubuntu

The ubuntu keys correspond to the parament of the apt repostory module, See: [apt_repository](https://docs.ansible.com/ansible/latest/modules/apt_repository_module.html)

The following parameters are required:

| Option | Comments                           |
| :----- | :--------------------------------- |
| name   | Sets the name of the source list   |
| repo   | A source string for the repository |

#### centos

The centos keys correspond to the parament of the yum repostory module and rpm key, See: [yum_repository](https://docs.ansible.com/ansible/latest/modules/yum_repository_module.html) and [rpm_key](https://docs.ansible.com/ansible/latest/modules/rpm_key_module.html)

The following parameters are required:

| Option  | Comments                                                            |
| :------ | :------------------------------------------------------------------ |
| name    | Sets the name of the baseurl                                        |
| baseurl | URL to directory where yum repository's 'repodata' directory lives. |

### defaults

```yml
repositories:
  ubuntu:
    - name: 'ubuntu universe'
      repo: >
        'deb http://archive.ubuntu.com/ubuntu
         {{ ansible_distribution_release | lower }} universe'
      state: present
    - name: 'ubuntu universe'
      repo: >
        'deb http://archive.ubuntu.com/ubuntu
         {{ ansible_distribution_release | lower }}-security universe'
      state: present
    - name: 'ubuntu universe'
      repo: >
        'deb http://archive.ubuntu.com/ubuntu
         {{ ansible_distribution_release | lower }}-updates universe'
      state: present
  centos:
    - name: 'epel'
      state: present
      description: 'EPEL YUM repo'
      baseurl: >
        https://download.fedoraproject.org/pub/epel/$releasever/$basearch/
      key: https://download.fedoraproject.org/pub/epel/RPM-GPG-KEY-EPEL-7
```

## Dependencies

None

## Example Playbook

```yml
- hosts: all
  roles:
    - arillso.repositories
```

## Author

- [Simon Bärlocher](https://sbaerlocher.ch)

## License

This project is under the MIT License. See the [LICENSE](licence) file for the full license text.

## Copyright

(c) 2020, Arillso
