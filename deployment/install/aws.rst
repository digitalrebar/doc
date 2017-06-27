.. index::
  pair: Linux; Run in AWS
  pair: AWS; Run in AWS
  pair: Deployment; Run in AWS

.. _run_in_AWS:

Run-In-AWS
==========

This is for installing in linux systems that are already out provisioned or taking over an existing Linux system.

See :ref:`initial_install_setup` for steps to checkout the DigitalRebar code and RackN deploy from ``digitalrebar/deploy`` directory.

**Note**: There must be a key based SSH access to the target system.  The install process logs into the system as root and will fix that access if there is a non-root account (specify with ``--login-user``).

Setting up the Server
*********************
This section will cover how to set up a server on Amazon and prime it for the install.

#. Create AWS m4.large (or larger!) Ubuntu instance.  This can be done with the SSH key or by following these steps:
	
	#. After logging in to AWS, click on EC2 under Compute. 
	#. Click on the button that says Launch Instance.  This will begin the initial setup for the server.
	#. Select Ubuntu Server for the AMI, then select ``m4.large`` or larger.
	#. Navigate to the Configure Security Group tab.  The recommended default Security Group for this server is Port 22 (ssh), 443 (rebar/HTTPS), 2375 & 2475 (docker), 4646 (chef), 8300 & 8301 (consul), 8888 (certificate signing service) and ICMP! However, this is just our recommended base.  Depending on the application, additional ports might be required, or Docker, Chef, and Consul may be omitted.  For more on this, see :ref:`port_mapping`.
	#. Launch the instance and save the ``.pem`` key as ``[key_name].pem`` to the home directory.  This can be done by using the ``gedit`` command, then copying and pasting the key to the new file. 

#. Once the server is launched, it can be connected to via the following command::

	ssh -i "[key_name].pem" ubuntu@[public_DNS]

Installing on the Server
************************
To install to the server, follow these steps.  Note: If already connected to the server, the first two steps can be omitted. 

#. Figure out the system IP address
#. If the root login is missing, then use ``./add-from-ssh`` to fix the credentials (our advanced scripts call this automatically)
#. ``./run-in-system.sh --help`` to make sure all of the pre-req's are in place
#. ``./run-in-system.sh --deploy-admin=[system|local] --admin-ip=[my CIDR ip/subnet]`` Choose ``system`` for remote install and ``local`` for the current system.
#. Allow the system to run and Ansible progress will be visible.
#. Follow steps to login to Digital Rebar UI.

Common Additional Options:

* If a ``~/.dr_info`` file is set up then ``workloads/add-provider.sh`` can be used to add providers by remote.
* If direct root control is not available, add ``--login-user=[username]``
* For a Metal or KVM booting dev-test add: ``--con-provisioner --access=FORWARDER``
* For a Docker test Compose scale command add: ``--con-node``

For troubleshooting tips and information, see :ref:`troubleshoot_aws`.
