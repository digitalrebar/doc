*********************
Digital Rebar Install
*********************

.. contents:: Table Contents
  :depth: 2

*Approximate install time: 10-30 minutes depending on bandwidth.*  Once cached, reset takes *3-10 minutes* on most systems.

**System Requirements** for Admin Container Host

* 8 Gb of RAM (or better) is recommended.
* 4 Physical Cores
* Operating System should be: Mac OSX or Linux

*Need help?* Jump over to our `live chat <https://gitter.im/digitalrebar/core>`_  (Gitter.im)

Jump to Specific Environments
-----------------------------

  * Already have a Linux system (VM or Physical)?  Use the `SSH <https://github.com/rackn/digitalrebar-deploy/edit/master/install/linux.rst>`_ helper or the `Local <https://github.com/rackn/digitalrebar-deploy/edit/master/install/local_linux.rst>`_ helper.
  * Don't have hardware?  No problem, we've got a quick install in `Packet.net <https://github.com/rackn/digitalrebar-deploy/blob/master/install_packet.rst>`_.
  * Use `Vagrant <https://github.com/rackn/digitalrebar-deploy/blob/master/install_vagrant.rst>`_? We've automated all these steps for that too. [**In progress**]
  * Comfortable with `Ansible <https://github.com/rackn/digitalrebar-deploy/edit/master/install/ansible.rst>`_? Deploy these steps automatically to Ubuntu and Centos.  They are the shared basis for the above helper scripts.

**RECOMMENDATION:** Review the `RackN maintained deploy scripts <https://github.com/rackn/digitalrebar-deploy>`_ for updated step-by-step install examples.

Provisioning from Containers
----------------------------

Digital Rebar operates all the infrastructure management functions in Docker containers; consequently, you need to be running in an environment that can run Docker.

    To improve support, the `Digital Rebar team <https://github.com/orgs/digitalrebar/teams>`_ is no longer creating or documenting install packages.

    For developers, we've collected some `additional guidance <development/advanced-install>`_ to review after you've got your first install working.

We are going to assume that you know how to use basic Docker and Docker Compose commands so that we can keep these instructions concise.  Please see the footnotes for command examples.

General Installation Steps
--------------------------

The general installation steps are described in the `Ansible <https://github.com/rackn/digitalrebar-deploy/edit/master/install/ansible.rst>`_ playbook docs.



