.. index::
  pair: Web UI; Networks

.. _ui_networks:

Networks
========

Digital Rebar has sophisticated networking for physical systems.  When changing networking settings, it is critical to understand the desired networking configuration.

Default Networks
----------------

When the :ref:`arch_service_provisioner` is enabled, Digital Rebar will include ``bmc-internal`` and ``admin-internal`` networks.  These are used for the boot infrastructure and node management.

Adding Networks
---------------

Networks are added by filling in the fields in the role on the networks table.

Network names are composites of their category and group.  This allows users to create networks that span regions and functions.  Networks must have unique names.

.. image:: /images/screens/dr_networks.png

They can be removed using the remove button.

Editing Networks
----------------

Once created, the edit screen allows users to make changes to the network configuration.

**Note**: These changes will not take effect until the matching node-roles are executed!

.. image:: /images/screens/dr_network_detail.png

To create a team, use a comma between the conduit codes.  E.g.: ``10g0, 10g1``

.. index:
  TODO; DNS_Filters
