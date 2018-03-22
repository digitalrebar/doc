
.. note:: WARNING WARNING WARNING:  This is the Digital Rebar v2 product documentation.  The v2 version is EOL as of September 2017.  Please refer to the new Digital Rebar Provision v3 documentation:  http:\/\/provision.readthedocs.io\/en\/tip\/README.html

.. index::
  pair: Services; DHCP
  pair: Services; DHCP Management
  pair: Containers; DHCP

.. _arch_service_dhcp:

DHCP
----

The DHCP container runs the Rebar DHCP server.  This is a customer DHCP server with a RestFUL API interface.
The container runs as a host-mode container, allowing the raw packets to be seen at the host.  The :ref:`arch_service_rebar_api`
container drives the construction of networks and binding of IPs to MAC addresses for the discovered nodes.

The DHCP server points the provisioning node to the :ref:`arch_service_provisioner` for installation and discovery.
