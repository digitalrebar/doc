.. index::
  Admin Node

.. _arch_other_systems:

Admin Node
----------

Currently, the Digital Rebar system is made up of a single Admin node.  This node can reside on a physical system
or virtual machine.  The main requirement is that Admin node be able to SSH into the managed nodes.

When the provisioner service is running, the nodes need to be able to access the Admin node with
provisioner web port and tftp.

When the DHCP service is running, the DHCP requests from the nodes' admin networks must get direct to the
Admin node.  This can be done by have the Admin node in the admin network or a DHCP forwarder to the 
Admin node.

When the Chef Jig is used, the managed nodes need to have access to the Admin Node's Chef Server.

In the future, multiple admin nodes will be allowed for redundancy and high availablity.

