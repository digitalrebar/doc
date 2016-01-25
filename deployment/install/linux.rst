Run-In-System for Linux System
==============================

This is for install in linux systems that are already out provisioned or to take over an existing Linux system.  

Follow the ../install.rst steps to checkout the DigitalRebar code and RackN deploy.

From ``digitalrebar/deploy`` directory

NOTE: You must have key based SSH access to your target system.  The install process logs into your system as root AND will fix that access if you have a non-root account (specify with ``--login-user``)

Here are the steps:

#. Figure out your system IP address
#. If you don't have root login, then use ``./add-from-ssh`` to fix your credentials (our advanced scripts call this automatically)
#. ``./run-in-system.sh --help`` to make sure we have all the pre-req's
#. ``./run-in-system.sh --deploy-admin=[system|local] --admin-ip=[my CIDR ip/subnet]`` Choose ``system`` for remote install and ``local`` for your current system.
#. Allow the system to run and you will see Ansible progress
#. Follow steps to login to Digital Rebar UI.

Common Additional Options:

* If you setup a ``~/.dr_info`` file then you can use ``workloads/add-provider.sh`` to add providers by remote.
* if you don't have direct root control, add ``--login-user=[username]``
* for a Metal or KVM booting dev-test add: ``--con-provisioner --access=FORWARDER``
* for a Docker test Compose scale command add: ``--con-node``

Regular Use & Dev Systems
~~~~~~~~~~~~~~~~~~~~~~~~~

These scripts are mainly used for single pass setups where you plan to tear down the system after use.  If you are planning to do regular development or 

