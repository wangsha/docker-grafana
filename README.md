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
that can be overridden. Full list of environment variables can be found [here](http://docs.grafana.org/installation/configuration/)

Sample configuration allowing github signup.
```yaml
- role: docker-grafana
      docker_grafana_ports:
        - 8080:3000
      docker_grafana_env:
        GF_SECURITY_ADMIN_USER: myadmin
        GF_SECURITY_ADMIN_PASSWORD: myadmin
        GF_USERS_ALLOW_SIGN_UP: true
        GF_SERVER_ROOT_URL: http://localhost:8080/
        GF_AUTH_GITHUB_ALLOW_SIGN_UP: true
        GF_AUTH_GITHUB_ENABLED: true
        GF_AUTH_GITHUB_SCOPES: user:email,read:org
        GF_AUTH_GITHUB_CLIENT_ID: XXXX
        GF_AUTH_GITHUB_CLIENT_SECRET: XXXX
        GF_AUTH_GITHUB_ALLOWED_ORGANIZATIONS: yourgithuborganization
```

If you need a playbook to set Docker itself, have a look at [angstwad.docker_ubuntu](https://github.com/angstwad/docker.ubuntu) Galaxy role.

Default docker image used is [grafana/grafana](https://hub.docker.com/r/grafana/grafana/). Default port is 3000, admin account `admin/admin`.


Custom volume mappings
----------------------
Docker allows mounting a host directory or a host file as [data volume](https://docs.docker.com/engine/userguide/containers/dockervolumes/).
This role mounts host directories to persist container data and host files to configure container behavior.
`docker_grafana_directory_volumes` and `docker_grafana_file_volumes` are the two variables to control volume mappings.
If you wish to customize the mapping, please follow `<host directory>:<container directory>:<mapping mode>` format
 to ensure host directories are correctly created before launching containers.
 
To customize host file mappings, update `docker_grafana_file_volumes`. 
This role will automatically create file parent directories and copy the template 
to host machine. The naming convention for template is `<host_file_name>.<host_file_extension>.j2`.
To copy template from your own ansible diretories, set `docker_grafana_template_path`.

Example Config:
```yaml
docker_grafana_file_volumes:
  - '/opt/myapp/conf/settings.conf:/etc/myapp/conf/settings.conf:ro'
docker_grafana_template_path: /path/to/ansible/project/templates/
# make sure file /path/to/ansible/project/templates//settings.conf.j2 exists. 
```


Additional References
---------------------
- [default docker image](https://hub.docker.com/r/grafana/grafana/)
- [dockerfile](https://github.com/grafana/grafana-docker)
- [docker image documentation](http://docs.grafana.org/installation/docker/)


License
-------

[MIT](LICENSE.txt)

Author Information
------------------

- wangsha
