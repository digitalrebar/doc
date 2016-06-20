.. index::
  pair: Services; DHCP
  pair: Services; DHCP Management
  pair: Containers; DHCP

.. _arch_service_dhcp:

DHCP
----

The dhcp container runs the rebar DHCP server.  This is a customer DHCP server with a RestFUL API interface.
The container runs as a host-mode container so that raw packets can be seen at the host.  The Rebar API 
container drives the construction of networks and binding of IPs to MAC addresses for discovered nodes.

The DHCP server points the provisioning node to provisioner for installation and discovery.

