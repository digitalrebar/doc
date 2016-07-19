Run-In-System
=============

This is for install in linux systems that are already out provisioned or to take over an existing Linux system.  

Follow the ../install.rst steps to checkout the DigitalRebar code and RackN deploy.

From ``digitalrebar/deploy`` directory

NOTE: There must be a key based SSH access to the target system.  The install process logs into the system as root AND will fix that access if there is a non-root account (specify with ``--login-user``)

Here are the steps:

#. Figure out the system IP address
#. If the root login is missing, then use ``./add-from-ssh`` to fix the credentials (our advanced scripts call this automatically)
#. ``./run-in-system.sh --help`` to make sure all of the pre-req's are in place
#. ``./run-in-system.sh --deploy-admin=[system|local] --admin-ip=[my CIDR ip/subnet]`` Choose ``system`` for remote install and ``local`` for the current system.
#. Allow the system to run and Ansible progress will be visible
#. Follow steps to login to Digital Rebar UI.

Common Additional Options:

* If a  ``~/.dr_info`` file is set up then ``workloads/add-provider.sh`` can be used to add providers by remote.
* If direct root control is not avalible, add ``--login-user=[username]``
* For a Metal or KVM booting dev-test add: ``--con-provisioner --access=FORWARDER``
* For a Docker test Compose scale command add: ``--con-node``

Regular Use & Dev Systems
~~~~~~~~~~~~~~~~~~~~~~~~~

These scripts are mainly used for single pass setups where the system is to be destroyed after use.  If you are planning to do regular development or 

