Networks
========

Digital Rebar has sophisticated networking for physical systems.  When changing networking settings it is critical to understand the desired networking configuration.

Default Networks
----------------

When the Provisioner is enabled, Digital Rebar will include ``bmc-internal`` and ``admin-internal`` networks.  These are used for the boot infrastructure and node management.

Adding Networks
---------------

Networks are added by filling in the fields in the role on the networks table.  

Network names are composites of their category and group.  This allows users to create networks that span regions and functions.  Networks must have unique names.

.. image:: /images/screens/dr_networks.png

They can be removed using the remove button.

Editing Networks
----------------

Once created, the edit screen allows users to make changes to the network configuration.  

NOTE: These changes will not take effect until the matching node-roles are executed!

.. image:: /images/screens/dr_network_detail.png

To create a team, use a comma between the conduit codes.  E.g.: ``10g0, 10g1``

Network Node Map
----------------

To help track network assignment, the network-node page helps show which nodes are assigned to each network.

.. image:: /images/screens/dr_network_node.png

This is a read only display.

Bus Interfaces
--------------

To cope with NIC enumeration differences between systems, it is possible to define custom bus mappings in Digital Rebar.

.. image:: /images/screens/dr_bus_interfaces.png

Developer Note: If creating a general mapping for new hardware types, please submit a pull request so that the mapping is included in the default list.

DNS Filters
-----------

Digital Rebar will automatically create DNS entries for nodes when they are created and remove them when they are destroyed.  The DNS filters allows users to define additional naming patterns based on the matcher patterns and templates.

.. image:: /images/screens/dr_dns_filters.png

.. index:
  TODO; DNS_Filters