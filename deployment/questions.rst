.. index::
  pair: Deployment; Questions to Consider

.. _deploy_questions:

Questions to Guide Deployment
-----------------------------

*Need help?* Jump over to our `live chat <https://gitter.im/digitalrebar/core>`_.

The goal of this set of questions is to help determine what containers to include during deployment, what workloads should be brought in,
and what tool must be running to deploy the admin node.

Whatcha' Doin' Questions
========================

The first thing to do is figure out what purpose Digital Rebar will serve.  This will
determine what must be installed, where it should be installed to, and what must be configured.

What Systems Do I Have to Play With?
====================================

With physical systems, fiddling with metal is an option.  Without physical systems, the cloud provider will allow systems to be run.

Are Metal Installs likely?
==========================

If bare metal servers are being managed, the :ref:`arch_service_provisioner` and :ref:`arch_service_dhcp`  containers will need to be included.
(See the :ref:`dhcp_or_not` for that question.)

.. index:
  TODO; chef-jig-ref
  TODO; arch_network_layout
  TODO; arch_providers_cloud

When managing metal, Digital Rebar uses the :ref:`chef_jig` for some actions. Therefore, it is required that nodes be able to communicate with the admin node.  If this is not possible, the network layout and  :ref:`arch_network_layout` will need to be rethought.

Are Cloud Instances Going to be Managed?
========================================

If the :ref:`arch_providers_cloud` is intended for use, the admin node must be able to access the cloud providers
and the credentials of the clouds.  The admin node and managed nodes can be live in a cloud.


Admin Node Questions
====================

With the intent of the operation determined, an :ref:`arch_other_systems` is required.
The admin node can run in the cloud, a VM, or a physical node.  The admin node has some
specific requirements.

System Requirements
+++++++++++++++++++

* 8 Gb of RAM (or more) is recommended.
* 4 Physical Cores
* Operating System should be: Mac OSX or Linux

Network Requirements
++++++++++++++++++++

The admin node needs to be able to talk to the internet in order to receive packages and other install components.  The admin node needs to
also be able to ssh into all nodes that it will manage.


What System Do I Have to Have to Run an Admin Node?
"""""""""""""""""""""""""""""""""""""""""""""""""""

An admin node needs a Docker capable system to run in.  This can be a Linux system with Docker-engine installed or on a MacOS with Docker tools installed.  In theory, a windows box could be used with virtual box and the Docker tools, but this isn't recommended.

For a Linux system, be certain to reference the `run-in-system.sh <https://github.com/digitalrebar/doc/blob/master/deployment/install/linux.rst>`_ script and its description.  This script can be run against the local system with the --localhost option or a remote system (with ssh access).

For a Mac system, be certain to reference the `run-in-mac.sh <https://github.com/digitalrebar/doc/blob/master/deployment/install/mac.rst>`_ script and its description.  This script will make sure that tools are installed to run Docker in a VirtualBox instance and allow the developer tools to run or the deploy tools against it.

For AWS or Packet, look at the *run-in-[aws|packet]* scripts.  They will automatically provision systems from those clouds and then install Digital Rebar.

What Access Mode Should I Use?
""""""""""""""""""""""""""""""

There are two access modes for Digital Rebar: HOST or FORWADER.  Most tools take a --host (or --access host) to specify host mode.  Forwarder mode is the default for all tools except run-in-mac.sh which has a --no-host flag to set forwarder mode.  Macs work best in HOST mode.  The mode can also be chosen in the group_vars/all.yml file. The ansible playbook is used to deploy the system. (or tools that use the playbook, which is all of them).

.. index::
  pair: Access Mode; Forwarder Mode

Forwarder Mode
##############

The Forwarder mode utilizes forwarder container that acts as the main access point for all Admin services.  The IP address of the forwarder is specified in the group_vars/all.yml file and is propagated to all the needed places.  The External IP should be set to match this value as well.  The primary use case is development on a single system with KVM or Docker instances for Digital Rebar to manage.  This mode can also be used to bridge secondary interfaces into the Docker bridge to provision physical machines on that network.

This mode requires an admin network, defined in compose/config-dir/api/config/networks/the_admin.json.forwarder, and a bmc network, defined in compose/config-dir/api/config/networks/the_bmc.json.forwarder.  Editting these to match and contain the FORWARDER_IP is required for a working deployment.  The default networks are 192.168.124.0/24 for the admin network and 192.168.128.0/24 for the BMC network.  The default forwarder ip is 192.168.124.11.  For bridged networks, it is assumed that 192.168.124.1 is the router on that network and that another address will be assigned to the docker0 bridge (like 192.168.124.200) and the physical interface (like eth1) will be added to the docker0 bridge.  This would allow physical nodes on the eth1 network to PXE boot and be discovered by the Admin node.

The developer tool, kvm-slave, works on a Linux-based system to add kvm slaves that run against the admin.

.. index::
  pair: Access Mode; Host Mode

Host Mode
#########

Host mode makes one of the host's addresses the access point for the Admin node.  This is useful for systems that are managing multiple admin networks, joined nodes (VMs or physical nodes), or dedicated hosts.  The Mac system falls into this case because the boot2docker image is akin to a separate node running a Docker system.

This mode requires an admin network, defined in compose/config-dir/api/config/networks/the_admin.json.mac.  The current defaults are 192.168.99.0/24.

Instead of specifying the Forwarder IP, the external IP must be specified for use.  This should be an IP on the host and does NOT have to be in the admin network.  The default is 192.168.99.100 to make the Mac deploy defaults.

For either mode, the FORWARDER_IP, EXTERNAL_IP, and mode is specified as values in the group_vars/all.yml file and some of the commands take those values as flags.

At this point, tools should be available, and the installation and deployment of Digital Rebar can begin.  Once installed and configured, nodes can be provisioned (using PXE of a physical system or creation of a kvm-slave) or joined (using add-from-system.sh) to the admin node.

Am I going to develop Digital Rebar or Workloads for Digital Rebar?
"""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""

Using the deploy tools, the environment should be setup for development as well.  The Docker-admin tools provided in core can be used to start and stop Digital Rebar containers.  It has a shell wrap that allows for quickly stopping, cleaning up, and restarting.

::

  cd digitalrebar/core
  tools/docker-admin

This creates a show where Docker-compose logs and other Docker commands can be run in order to inspect the containers.  Exiting this shell will remove and kill the containers.  *Docker-admin* takes an --access flag with a value of either HOST or FORWARDER and a very helpful ``--no-pull`` flag that prevents a pull update to increase iteration speeds.


The ``run-in-[packet|system|google|docean|aws].sh [options]`` or ``workloads\[kubernetes]`` scripts will quickly build a working Digital Rebar administration system.  There are advanced workload scripts that will setup Digital Rebar and provision a workload.

The :ref:`arch_service_provisioner`/:ref:`arch_service_dhcp` containers (include with ``--con-provisioner --con-dhcp``) are able to handle DHCP/PXE boot discovery of metal and KVM.  These options will lengthen the install because they download previsioning ISOs from source.  ISO can automatically be updated from a local``~/digitalrebar/isos``.

The cloud providers require an account with the provider.  For first users AWS, Google, or Packet are recommended.
