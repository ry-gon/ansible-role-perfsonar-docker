perfsonar-docker
=========

Install the perfsonar toolkit or testpoint as a docker container, as sourced from https://hub.docker.com/r/perfsonar.

Role Variables
--------------

Default role variables are found in `defaults/main.yml`.

| Name       | Default Value | Description |
| ---------- | ------------- | ----------- |
| `perfsonar_docker_bundle` | "" | Choice of `testpoint` or `tools`. This is required. |
| `perfsonar_docker_ntp_servers` | "" | List of ntp servers to add to the container's /etc/ntp.conf |

Dependencies
------------

Docker must be installed properly for this role to function as it should. The role found at
https://galaxy.ansible.com/mongrelion/docker/ can be quite useful for its installation.

Example Playbook
----------------

```
- hosts: testpoints
  roles:
    - { role: ry-gon.perfsonar-docker, perfsonar_docker_bundle: testpoint }

- hosts: toolkits
  roles:
    - { role: ry-gon.perfsonar-docker, perfsonar_docker_bundle: tools }
```

Full Containerized perfSONAR Installation from a fresh CentOS/EL Guide:
----------------------------------------------------

First install the necessary packages:
```
yum -y install ansible
ansible-galaxy -f install mongrelion.docker
ansible-galaxy -f install ry-gon.perfsonar-docker
```

Then write a simple playbook to call the roles. The one shown below will provide a standard installation with the 'perfsonar-testpoint' bundle.
```
- hosts: testpoints
  roles:
    - { role: mongrelion.docker }
    - { role: ry-gon.perfsonar-docker, perfsonar_docker_bundle: testpoint }
```

Note that the system's clock must be in sync for perfSONAR to function properly. This can be set through ntp, with a command such as:
```
ntpdate [ntp server]
```

The container should be up and running by default. To attach to it, run the following:
```
docker exec -it perfsonar_testpoint /bin/bash
```
If the tools bundle is used, it would be `perfsonar_tools` instead of `perfsonar_testpoint`.

From here, you can run any regular perfsonar commands, such as `pscheduler`.

To stop or start the container, run:
```
docker container stop perfsonar_testpoint
```
or
```
docker container start perfsonar_testpoint
```
and to list all containers (started or stopped), run:
```
docker container ls -a
```

License
-------

Apache 2.0

Author Information
------------------

Written by Ryan Goniwiecha 
http://gitlab.com/ry-gon
