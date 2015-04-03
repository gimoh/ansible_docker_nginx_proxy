[![ansible-galaxy gimoh.docker_nginx_proxy](https://img.shields.io/badge/ansible--galaxy-gimoh.docker__nginx__proxy-brightgreen.svg)](https://galaxy.ansible.com/list#/roles/3097) [![License GPLv3](https://img.shields.io/badge/license-GPLv3-blue.svg)](http://www.gnu.org/licenses/gpl-3.0.html)

Role Name
=========

Role for deploying an nginx proxy container based on
[jwilder/nginx-proxy](https://registry.hub.docker.com/u/jwilder/nginx-proxy/)
docker image.

This image provides an optional automatic reverse-proxy for any container
started on the same host.  See description on Docker Hub for details.

I'm using this with role
[gimoh.docker_container](https://galaxy.ansible.com/list#/roles/3101) which
wraps `docker` module and creates/starts containers and can optionally mark
the container to be registered with the proxy provided by this role, as well
as upload SSL/TLS certificates for use by the proxy.

Requirements
------------

- [Docker](https://www.docker.com/), I personally use the role
  [angstwad.docker_ubuntu](https://galaxy.ansible.com/list#/roles/292) to
  deploy it

Role Variables
--------------

_defaults/main.yml_

```
# Path to directory *on the host* where SSL/TLS certificates for the exposed
# services will be stored.  This path is mounted as a volume into the
# nginx-proxy container so nginx can access the certificates.  The private
# keys and certificates stored there should be named after the FQDN of the
# service with .key and .crt extension respectively.
#
# This role will create and ensure correct permissions on that directory.
#
# See description of the jwilder/nginx-proxy docker image for details.
dnp_nginx_certs_dir: /etc/pki/svc-certs

# Path to directory *on the host* where nginx per-vhost configuration
# file fragments will be stored.  This path is mounted as a volume into
# the nginx-proxy container so nginx can access the files.
dnp_nginx_vhost_dir: /etc/nginx-proxy-vhost.d
```

Dependencies
------------

- a role to set up docker, as mentioned I use
  [angstwad.docker_ubuntu](https://galaxy.ansible.com/list#/roles/292), there
  is no hard dependency as this role isn't Ubuntu-specific

Example Playbook
----------------

This demonstrates how to deploy the image on a base Ubuntu server:

    - hosts: servers
      sudo: True
      roles:
         - willshersystems.apt
         - angstwad.docker_ubuntu
         - gimoh.docker_nginx_proxy

License
-------

GPLv3

Author Information
------------------

Contact me through GitHub issues, etc.

gimoh
