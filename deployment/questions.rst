.. _deploy_questions:

Questions to Guide Deployment
-----------------------------

*Need help?* Jump over to our `live chat <https://gitter.im/digitalrebar/core>`_  (Gitter.im)

**System Requirements** for Admin Container Host

* 8 Gb of RAM (or better) is recommended.
* 4 Physical Cores
* Operating System should be: Mac OSX or Linux


Providers: What Systems Do I Have to Play With?
"""""""""""""""""""""""""""""""""""""""""""""""

The ``run-in-[packet|system|google|docean|aws].sh [options] `` or ``workloads\[docker-swarm|kubernetes]`` scripts will quickly build a working Digital Rebar administrate system.  There are advanced workload scripts that will setup Digital Rebar AND provision a workload.

The Provisioner/DHCP containers (include with ``--con-provisioner --con-dhcp``) are able to handle DHCP/PXE boot discovery of metal and KVM.  These options will lengthen the install because they download provioning ISOs from source.  You can also automatically upload ISOs from your local ``~/digitalrebar/isos``.

The cloud providers require that you have an account with the provider.  For first users, we recommend AWS, Google or Packet.

What System Do I Have to Run an Admin Node?
"""""""""""""""""""""""""""""""""""""""""""

An admin node needs a docker capable system to run in.  This can be a Linux system with docker-engine installed or a MacOS with docker tools installed.  In theory, a windows box could be used with virtual box and the docker tools, but come on.

For a linux system, you will want to look at the `run-in-system.sh <https://github.com/digitalrebar/doc/blob/master/deployment/install/linux.rst>`_ script and its description.  This script can be run against the local system with the --localhost option or a remote system (with ssh access).

For a Mac system, you will want to look at the `run-in-mac.sh <https://github.com/digitalrebar/doc/blob/master/deployment/install/mac.rst>`_ script and its description.  This script will make sure that tools are installed to run docker in a VirtualBox instance and let you run the developer tools or the deploy tools against it.

For AWS or Packet, look at the *run-in-[aws|packet]* scripts.  They will automatically provision systems from those clouds and then install Digital Rebar.

What Access Mode Should I Use?
""""""""""""""""""""""""""""""

There are two access modes for Digital Rebar: HOST or FORWADER.  Most tools take a --host (or --access host) to specify host mode.  Forwarder mode is the default for all tools except run-in-mac.sh which has a --no-host flag to set forwarder mode.  Macs work best in HOST mode.  The mode can also be choosen in the group_vars/all.yml file run the ansible playbook is used to deploy the system (or tools that use the playbook - which is all of them).

Forwarder Mode
##############

This mode uses a forwarder container to act as the main access point for all Admin services.  The IP address of the forwarder is specified in the group_vars/all.yml file and gets propogated to all the needed places.  The External IP should be set to match this value as well.  The primary use case is for development on a single system with KVM or docker instances for Digital Rebar to manage.  This mode can also be used to bridge secondary interfaces into the docker bridge to provision physical machines on that network.

This mode requires an admin network, defined in compose/config-dir/api/config/networks/the_admin.json.forwarder, and a bmc network, defined in compose/config-dir/api/config/networks/the_bmc.json.forwarder.  Editting these to match and contain the FORWARDER_IP is required for a working deployment.  The default networks are 192.168.124.0/24 for the admin network and 192.168.128.0/24 for the BMC network.  The default forwarder ip is 192.168.124.11.  For bridged networks, it is assumed that 192.168.124.1 is the router on that network and that another address will be assigned to the docker0 bridge (like 192.168.124.200) and the physical interface (like eth1) will be added to the docker0 bridge.  This would allow physical nodes on the eth1 network to PXE boot and be discovered by the Admin node.

The developer tool, kvm-slave, should work on linux-based system to add kvm slaves to run against the admin. 

Host Mode
#########

This mode makes one of the host's addresses the access point for the Admin node.  This is useful for systems that are managing multiple admin networks, lots of joined nodes (VMs or physical nodes), or dedicated hosts.  The Mac system falls into this cases because the boot2docker image is like a separate node running a docker system.

This mode requires an admin network, defined in compose/config-dir/api/config/networks/the_admin.json.mac.  The current defaults are 192.168.99.0/24.  It matches Greg Althaus' mac deployment (I took the defaults).  

Instead of specifying the Forwarder IP, we have to specify the external IP to use.  This should be an IP on the host and does NOT have to be in the admin network.  The default is 192.168.99.100 to make the Mac deploy defaults.

For either mode, the FORWARDER_IP, EXTERNAL_IP, and mode is specified as values in the group_vars/all.yml file or some of the commands take those values as flags.

At this point, you should be able to choose your tool and install and deploy Digital Rebar.  Once installed and configured, you can provision nodes (using good ole PXE of a physical system or creation of a kvm-slave) or join nodes (using add-from-system.sh) to the admin node.

Am I going to develop Digital Rebar or Workloads for Digital Rebar?
"""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""

Using the deploy tools, the environment should be setup for doing development as well.  You can switch to using the docker-admin tools provided in core to start and stop Digital Rebar containers.  It has a shell wrap that allows you to quickly stop, clean-up, and restart.

::

  cd digitalrebar/core
  tools/docker-admin
  
This leaves you in a show where you can run docker-compose logs and other docker commands to inspect the containers.  Exiting this shell will kill and remove the containers.  *docker-admin* takes an --access flag with a value of either HOST or FORWARDER and a very helpful ``--no-pull`` flag that doesn't do a pull update to increase iteration speeds.


