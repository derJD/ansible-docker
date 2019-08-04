docker
======

Installs docker-ce and manage configuration with [daemon.json](https://docs.docker.com/engine/reference/commandline/dockerd/#daemon-configuration-file).
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

There are a bunch of Variables which values depends on os:
* `docker_repo_url`
* `docker_key_id`
* `docker_key_url`
* `docker_pre_packages`

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
