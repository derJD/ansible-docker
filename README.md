docker
======

Installs docker-ce and docker-compose. This role manages daemon configuration as well via [/etc/docker/daemon.json](https://docs.docker.com/engine/reference/commandline/dockerd/#daemon-configuration-file).
I think it is a bit more convinient configuring the docker daemon with its configuration file instead of passing flags via environments.

Requirements
------------

none so far.

Role Variables
--------------

| Variable | Type | Default | Description |
| -------- | ---- | ------- | ----------- |
| `docker_daemon_options` | dict | `{group: docker, log-driver: journald}` | Dictionary containing all settings for daemon.json |
| `docker_packages` | list | `[docker-ce, docker-ce-cli, containerd.io, docker-compose]` | List containing packages which should be installed |
| `docker_os_skip_list` | list | `[CoreOS, Coreos]` | List of operatingsystems that don't require package installation |
| `docker_compose_service` | bool | `false` | If set to `true` a systemd service template for docker-compose files is created |

There are a bunch of Variables which values depends on os:
* `docker_repo_url`
* `docker_key_id`
* `docker_key_url`
* `docker_pre_packages`

**docker_compose_service**
* When enabled you can store docker-compose files in `/etc/docker/compose/` directory.
* For example: If you whish to start your example deployment, store it like this: `/etc/docker/compose/example.yml`
* And start it like this: `systemctl start docker-compose@example`
* You can update your deployment with this hack: `systemctl start docker-compose@example`

Dependencies
------------

none so far.

Example Playbook
----------------

* basic example:
```
---
- hosts: servers
  roles:
     - derJD.docker
```

* how config for my workstation would look like:
```
---
- hosts: workstation
  vars:
    docker_daemon_options:
      group: docker
      bip: 10.53.0.1/27
      log-driver: journald
      storage-driver: zfs
  roles:
     - derJD.docker
```

License
-------

BSD

Author Information
------------------

[derJD](https://github.com/derJD/)
