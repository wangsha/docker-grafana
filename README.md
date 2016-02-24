docker-grafana
============

[![Build Status](https://travis-ci.org/wangsha/docker-grafana.svg?branch=master)](https://travis-ci.org/wangsha/docker-grafana)
[![Ansible Galaxy](https://img.shields.io/badge/AnsibleGalaxy-wangsha.docker--grafana-blue.svg)](https://galaxy.ansible.com/wangsha/docker-grafana/)

Ansible role to manage and run the grafana docker container.

Requirements
------------

This role has only been tested on Ubuntu 14.04. Since this uses Ansible's
docker module, you will need to ensure that a recent-ish version of `docker-py`
and `docker` are installed.

Examples
--------

Install this module from Ansible Galaxy into the './roles' directory:
```bash
ansible-galaxy install wangsha.docker-grafana -p ./roles
```

Use it in a playbook as follows, assuming you already have docker setup:
```yaml
- hosts: 'servers'
  roles:
    - role: 'wangsha.docker-grafana'
      become: true
```

Have a look at the [defaults/main.yml](defaults/main.yml) for role variables
that can be overridden.

If you need a playbook to set Docker itself, have a look at [angstwad.docker_ubuntu](https://github.com/angstwad/docker.ubuntu) Galaxy role.

Default docker image used is [grafana/grafana](https://hub.docker.com/r/grafana/grafana/). Basic auth account `admin/admin`.


License
-------

[MIT](LICENSE.txt)

Author Information
------------------

- wangsha
