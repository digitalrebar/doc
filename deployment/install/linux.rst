Run-In-System for Linux System
==============================

This is for Lnstall in linux systems that are already out provisioned or to take over an existing Linux system.

Follow the ../install.rst steps to checkout the DigitalRebar code and RackN deploy.

From ``digitalrebar/deploy`` directory

NOTE: You must have key based _root_ SSH access to your target system.  The install process logs into your system as root.

1) Figure out your system IP address
2) ``./run-in-system.sh --help`` to make sure we have all the pre-req's
3) ``./run-in-system.sh --deploy-admin=[system|local] --admin-ip=[my CIDR ip/subnet]`` Choose ``system`` for remote install and ``local`` for your current system.
4) Allow the system to run and you will see Ansible progress
5) Follow steps to login to Digital Rebar UI.

Additional Options:

* for a KVM booting dev-test add: --con-provisioner --access=FORWARDER
* for a Docker test node add: --con-node

