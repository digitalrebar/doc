.. _ux_network:

Network
=======

Digital Rebar has sophisticated networking for physical systems.  When changing networking settings, it is critical to understand the desired networking configuration.

From the "Network" page, all the networks in deployment are visible, and their descriptions, categories, group, deployments, tenants, and conduits are displayed.


.. image:: /images/screens/webux/network.png

Default Networks
----------------

When the :ref:`arch_service_provisioner` is enabled, Digital Rebar will include ``bmc-internal`` and ``admin-internal`` networks.  These are used for the boot infrastructure and node management.

Adding Networks
---------------

Networks are added via the ``Add Network`` button in the bottom right hand corner.

Network names are composites of their category and group.  This allows users to create networks that span regions and functions.  Networks must have unique names.

.. image:: /images/screens/webux/networks.png

They can be removed by selecting a network and clicking the remove button.

Editing Networks
----------------

Once created, the edit screen allows users to make changes to the network configuration.

**Note**: These changes will not take effect until the matching node roles are executed!

.. image:: /images/screens/webux/edit_network.png

To create a team, use a comma between the conduit codes.  E.g.: ``10g0, 10g1``

