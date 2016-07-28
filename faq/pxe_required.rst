.. index::
	Server; Boot Setup

.. _faq_pxe_required:

Should the Server be Setup to Boot from PXE on All Available Nework Ports?
==========================================================================

As long as it will PXE boot to a DHCP server under our control (for now), and Rebar has been delegated an IP address to use for admin purposes, then our current node discovery workflow will handle configuring IPMI/DRAC/AMT.  Rebar was initially designed as a tool to take racks of servers from racked and cabled to running Openstack or Hadoop with minimal intervention, and configuring things like IPMI is part of that workflow that we have retained.

The Server should then be discovered, meaning it should end up in some sort of inventory that we can query that will tell us which hardware is available, Mac addresses etc.

All nodes that we manage wind up in a "system" deployment, and our API exposes that along with discovered attributes about that node.  
