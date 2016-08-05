.. index::
  pair: Linux; Run in Google
  pair: Deployment; Run in Google

.. _run_in_google:

Run-In-Google
=============

This is for install in linux systems that are already out provisioned or to take over an existing Linux system.

Follow the ../install.rst steps to checkout the DigitalRebar code and RackN deploy from ``digitalrebar/deploy`` directory.

NOTE: There must be a key based SSH access to the target system.  The install process logs into the system as root AND will fix that access if there is a non-root account (specify with ``--login-user``).

Here are the steps:

#. Figure out the system's IP address.
#. If the root login is missing, then use ``./add-from-ssh`` to fix the credentials (our advanced scripts call this automatically).
#. ``./run-in-system.sh --help`` to make sure all of the pre-req's are in place.
#. ``./run-in-system.sh --deploy-admin=[system|local] --admin-ip=[my CIDR ip/subnet] --access=HOST``. Choose ``system`` for remote install and ``local`` for the current system.
#. Allow the system to run. Ansible progress will be visible.
#. Follow steps to login to Digital Rebar UI.

Common Additional Options:

* If a ``~/.dr_info`` file is set up then ``workloads/add-provider.sh`` can be used to add providers by remote.
* If direct root control is not avalible, add ``--login-user=[username]``.
* For a Metal or KVM booting dev-test add: ``--con-provisioner --access=FORWARDER``.
* For a Docker test Compose scale command add: ``--con-node``.

Install tip: It is possible to connect to a Google VM via the Compute Engine page. Doing this will pull up a terminal in the web browser that is already connected to the VM. This makes connecting to the system simply and allows the install to be run with ``local``.

Sample install code for a Ubuntu system connected to via the Compute Engine page, including tool set up, is provided below. **Note:** It is necessary to replace [CIDR] in ``export IPA=[CIDR]`` with the system's CIDR, found in ``ip -4 addr``. If this is not done, the install will **not** work!
::

	sudo apt-get update
	sudo apt-get install git
	mkdir digitalrebar
	git clone https://github.com/rackn/digitalrebar-deploy digitalrebar/deploy
	ln -s digitalrebar/ digitalrebar/deploy/compose/digitalrebar
	cd digitalrebar/deploy
	./run-in-system.sh --help
	ip -4 addr
	export IPA=[CIDR]
	./run-in-system.sh --deploy-admin=local --admin-ip=$IPA --access=HOST

For troubleshooting tips and information, see :ref:`troubleshoot_google`.
