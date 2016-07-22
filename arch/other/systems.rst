.. index::
  Admin Node

.. _arch_other_systems:

Admin Node
----------

Currently, the Digital Rebar system is made up of a single admin node.  This node can reside on either a physical system
or a virtual machine.  Its main requirement is that the admin node must be able to SSH into the managed nodes.

When the :ref:`arch_service_provisioner` service is running, the nodes need to be able to access the admin node with
provisioner web port and TFTP.

When the :ref:`arch_service_dhcp` service is running, the DHCP requests from the nodes' admin networks must be direct to the
admin node.  This can be done by have the Admin node in the admin network or a DHCP forwarder to the Admin node.

When the :ref:`chef_jig` is used, the managed nodes need to have access to the admin node's Chef Server.

In the future, multiple admin nodes will be allowed for redundancy and high availablity.
