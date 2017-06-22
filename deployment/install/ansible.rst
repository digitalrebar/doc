Using the Ansible Playbook
--------------------------

The Digital Rebar `ansible <http://ansible.com>`_ playbook starts in `digitalrebar.yml <https://github.com/digitalrebar/digitalrebar/deploy/digitalrebar.yml>`_ and uses the `tasks <https://github.com/digitalrebar/digitalrebar/deploy/digitalrebar.yml/tasks>`_ and `group vars <https://github.com/digitalrebar/digitalrebar/deploy/group_vars/all.yml>`_ to drive configuration.

The playbook is driven by a set of "run-in-FOO" scripts handle accessing the system be it Linux-based (remote or local), Mac OSX, or in a metal provider (Packet).

Check the `scripts <https://github.com/digitalrebar/digitalrebar/deploy>`_ to see how to run the playbook.  *run-in-foo.sh*

A video guide on how to make changes to a single ansible script running in a role can be found at :ref:`training-ansible-edit`. 

What's installed?
=================
Installation requires several steps. To begin with, the following is done by default:

* All prerequisites including the latest Docker with correct permissions (instructions for some of these are included, just in case)
* Latest Digital Rebar code from develop branch
* Node target operating systems ISOs:
    * Ubuntu 16.04 and Centos 7 ISO
* Docker & Docker Compose to Run Digital Rebar Containers

Configuration settings are managed under ``deploy/compose/config-dir``

**Note:** It is strongly recommended to review the actively maintained `deploy scripts <https://github.com/digitalrebar/digitalrebar/deploy/>`_ to see the latest install process.


Housekeeping Notes
==================

To remove Docker image cruft, we suggest running ``docker ps -q -a | xargs docker rm`` on a regular basis.
