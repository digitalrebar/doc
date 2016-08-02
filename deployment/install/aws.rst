.. index::
  pair: Linux; Run in AWS
  pair: AWS; Run in AWS
  pair: Deployment; Run in AWS

.. _run_in_AWS:

Run-In-AWS
==========

This is for installing in linux systems that are already out provisioned or taking over an existing Linux system.

Follow the ../install.rst steps to checkout the DigitalRebar code and RackN deploy from ``digitalrebar/deploy`` directory.

*NOTE*: There must be a key based SSH access to the target system.  The install process logs into the system as root and will fix that access if there is a non-root account (specify with ``--login-user``).


Here are the steps:

#. Figure out the system IP address
#. If the root login is missing, then use ``./add-from-ssh`` to fix the credentials (our advanced scripts call this automatically)
#. ``./run-in-system.sh --help`` to make sure all of the pre-req's are in place
#. ``./run-in-system.sh --deploy-admin=[system|local] --admin-ip=[my CIDR ip/subnet]`` Choose ``system`` for remote install and ``local`` for the current system.
#. Allow the system to run and Ansible progress will be visible
#. Follow steps to login to Digital Rebar UI.

Common Additional Options:

* If a ``~/.dr_info`` file is set up then ``workloads/add-provider.sh`` can be used to add providers by remote.
* If direct root control is not avalible, add ``--login-user=[username]``
* For a Metal or KVM booting dev-test add: ``--con-provisioner --access=FORWARDER``
* For a Docker test Compose scale command add: ``--con-node``

For troubleshooting tips and information, see :ref:`roubleshoot_aws`.
