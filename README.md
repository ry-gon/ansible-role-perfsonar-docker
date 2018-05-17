Role Name
=========

Install the perfsonar toolkit as a docker container, as sourced from https://hub.docker.com/r/perfsonar/tools/.

Requirements
------------

Any pre-requisites that may not be covered by Ansible itself or the role should be mentioned here. For instance, if the role uses the EC2 module, it may be a good idea to mention in this section that the boto package is required.

Role Variables
--------------

A description of the settable variables for this role should go here, including any variables that are in defaults/main.yml, vars/main.yml, and any variables that can/should be set via parameters to the role. Any variables that are read from other roles and/or the global scope (ie. hostvars, group vars, etc.) should be mentioned here as well.

Dependencies
------------

Docker must be installed properly for this role to function as it should. The role found at
https://galaxy.ansible.com/mongrelion/docker/ can be quite useful for its installation.

Example Playbook
----------------

Including an example of how to use your role (for instance, with variables passed in as parameters) is always nice for users too:

- hosts: testpoints
  roles:
     - { role: ry-gon.perfsonar-docker, perfsonar-docker-bundle: testpoint }

- hosts: toolkits
  vars_files:
    - vars/perfsonar_vars.yml
  roles:
     - { role: ry-gon.perfsonar-docker, perfsonar-docker-bundle: tools }

License
-------

Apache 2.0

Author Information
------------------

Written by Ryan Goniwiecha http://github.com/ry-gon
