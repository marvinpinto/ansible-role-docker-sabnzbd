docker-sabnzbd
==============

[![Build Status](https://img.shields.io/travis/marvinpinto/ansible-role-docker-sabnzbd/master.svg?style=flat-square)](https://travis-ci.org/marvinpinto/ansible-role-docker-sabnzbd)
[![Ansible Galaxy](https://img.shields.io/badge/ansible--galaxy-docker--sabnzbd-blue.svg?style=flat-square)](https://galaxy.ansible.com/marvinpinto/docker-sabnzbd)
[![License](https://img.shields.io/badge/license-MIT-brightgreen.svg?style=flat-square)](LICENSE.txt)

Ansible Galaxy role to manage and run a [sabnzbd](http://sabnzbd.org) docker
container.

This role wires together the sabnzbd [docker
container](https://hub.docker.com/r/linuxserver/sabnzbd) created by
[linuxserver](https://github.com/linuxserver/docker-sabnzbd), along with
various boilerplate to get things going.


Requirements
------------

This role has been tested on Ubuntu 14.04 and will likely only work on an
Ubuntu-like system. You will also need a functioning docker environment and a
recent-is version of `docker-py` for this role to work.

If you have neither and would like ansible to set this up for you, have a look
at the [marvinpinto.docker](https://galaxy.ansible.com/marvinpinto/docker)
Galaxy role.


Role Variables
--------------

```yaml
# Sabnzbd host port
docker_sabnzbd_exposed_port: '8080'

# Docker container name
docker_sabnzbd_container_name: 'sabnzbd'

# Directory that will be used as the root of all sabnzbd-related configuration
# & data. Note that these sub-directories *will* be automatically created if
# they don't already exist.
#
# So, assuming 'docker_sabnzbd_mounted_directory' is set to:
# /tmp/sabnzbd_mount, the following directories will be created automatically:
# /tmp/sabnzbd_mount/config
# /tmp/sabnzbd_mount/downloads
# /tmp/sabnzbd_mount/incomplete-downloads
docker_sabnzbd_mounted_directory: '/tmp/sabnzbd_mount'
```


Examples
--------

Install this module from Ansible Galaxy into the './roles' directory:
```bash
ansible-galaxy install marvinpinto.docker-sabnzbd -p ./roles
```

Use it in a playbook as follows:
```yaml
- hosts: '127.0.0.1'
  roles:
    - role: 'marvinpinto.docker-sabnzbd'
      become: true
```


Mounted Directory
-----------------

The reasoning behind storing all related configuration in the
`docker_sabnzbd_mounted_directory` root directory is because a person now has
the ability to manage all the configuration + data outside of Ansible.

This becomes especially useful when said mounted directory resides on a
separate filesystem (EBS, USB disk, etc).
