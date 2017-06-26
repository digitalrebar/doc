.. index::
  pair: Linux; Run in System
  pair: Deployment; Run in System

.. _run_in_system:

Run-In-System
-------------

This guide is to install in Linux systems that are already out provisioned or to take over an existing Linux system.

Follow the ../install.rst steps to checkout the DigitalRebar code and RackN deploy from ``digitalrebar/deploy`` directory.

**Note**: There must be a key based SSH access to the target system.  The install process logs into the system as root AND will fix that access if there is a non-root account (specify with ``--login-user``)

Here are the steps:

#. Use the commands ``ip -4 addr`` and ``export IPA=[CIDR]`` to find and save the CIDR (The external IP and the /XX Subnet address).
#. If the root login is missing, then use ``./add-from-ssh`` to fix the credentials (our advanced scripts call this automatically).
#. ``./run-in-system.sh --help`` to make sure all of the pre-req's are in place.
#. ``./run-in-system.sh --deploy-admin=[system|local] --admin-ip=[my CIDR ip/subnet]`` Choose ``system`` for remote install and ``local`` for the current system.
#. Allow the system to run.  Ansible progress will be visible.
#. Follow steps to login to Digital Rebar UI.

Common Additional Options:

* If a  ``~/.dr_info`` file is set up, then ``workloads/add-provider.sh`` can be used to add providers by remote.
* If direct root control is not available, add ``--login-user=[username]``.
* For a Metal or KVM booting dev-test add: ``--con-provisioner --access=FORWARDER``.
* For a Docker test Compose scale command add: ``--con-node``.
* To avoid ISO downloads, you can push ISOs from your install system in the tftpboot/isos directory instead of the public repos.  You _must_ rename ``copy_isos.no`` to be ``copy_isos.yes`` for this feature to work.

For troubleshooting, see :ref:`troubleshoot_run_in_system` for help.

Sample code for a complete install with setup included is provided below. 

**Note**: [CIDR] in ``export IPA=[CIDR]`` must be replaced with the system's CIDR, found with the command ``ip -4 addr``.  If this is not done, the install will **not** work!

Debian/Ubuntu:

::

	sudo apt-get update
	sudo apt-get install git
	mkdir digitalrebar
	git clone https://github.com/digitalrebar/digitalrebar
	cd digitalrebar/deploy
	ip -4 addr
	export IPA=[CIDR]
	./run-in-system.sh --help
	sudo ./run-in-system.sh --deploy-admin=local --access=host --admin-ip=$IPA

Centos/Red Hat
::

	sudo yum update
	sudo yum install -y git
	cd 
	git clone https://github.com/digitalrebar/digitalrebar
	cd digitalrebal/deploy
	ip -4 addr
	export IPA=[CIDR]
	sudo ./run-in-system.sh --deploy-admin=local --access=host --admin-ip=$IPA

