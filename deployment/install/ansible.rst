##################################################
Using the `Ansible <http://ansible.com>`_ Playbook
##################################################

The Digital Rebar playbook starts in `digitalrebar.yml <https://github.com/rackn/digitalrebar-deploy/digitalrebar.yml>`_ and uses the `tasks <https://github.com/rackn/digitalrebar-deploy/tasks>`_ and `group vars <https://github.com/rackn/digitalrebar-deploy/group_vars>`_ to drive configuration.

The playbook is driven by a set of scripts handle accessing the system be it linux-based (remote or local), Mac OSX, or in a metal provider (Packet).

Check the `scripts <https://github.com/rackn/digitalrebar-deploy>`_ to see how to run the playbook.  *run-in-xxx.sh*

What's installed?
"""""""""""""""""

The following is done by default:

  * all prerequisites including latest Docker with correct permissions
  * latest Digital Rebar code from develop branch
  * Node target operating systems:
     * Ubuntu 14.04 and Centos 7 ISO
  * Default IP maps for Digital Rebar: 
     * internal address of 192.168.124.11
     * port mapping of UI (:3000) and Consul (:8500)

All of these can be altered by the group_vars/all.yml.

Configuration Options
"""""""""""""""""""""

The following options are available to be modified in the `group_vars/all.yml <https://github.com/rackn/digitalrebar-deploy/group_vars/all.yml>`_ file.  The file contains documentation for each var, but additional detail is specified in the table below.

+---------------+----------+-----------+---------+
| *Key*         | *Values* | *Default* | *Notes* |
+---------------+----------+-----------+---------+
| dr_services   |          |           |         |
|               |          | jj        | jj      |
+---------------+----------+-----------+---------+
| dr_workload   | jj       | jj        |         |
+---------------+----------+-----------+---------+


.. code-block:: shell

  <h1>code block example</h1>
