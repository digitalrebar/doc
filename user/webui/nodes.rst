.. index::
  pair: Web UI; Nodes

.. _ui_nodes:

Nodes
=====

Nodes are a core element of the Digital Rebar system.

.. image:: /images/screens/dr_nodes_provider_enabled.png

No Single State
---------------

Digital Rebar does not maintain a single node state; instead, state is composed from the node-roles that are assigned to the node.

As a convenience, these states are summarized for users:

  * If all states are ready, then the node is considered ready.
  * If any are error, then the node is considered in error.
  * If any are proposed, then the node is considered proposed.
  * Any other state, then the node is considered in transition.

Additional States
-----------------

Nodes have several override conditions that prevent Digital Rebar from operating on them.  These conditions are powered-off and reserved.  If these states are true, Digital Rebar will not attempt to use the node.


Cloud Nodes
-----------

Digital Rebar can create/destroy nodes on external "cloud" systems using the :ref:`ui_providers` system.

Physical Nodes
--------------

Once the Digital Rebar Admin is running, simply booting VMs or physical nodes
onto the management network will engage the discovery process (using
:ref:`arch_service_dhcp` and PXE). Digital Rebar does not event hook the PXE service (to maintain
separation of duties), so please be patient. The default discovery
process requires the system to boot the Sledgehammer image, which
takes time.

Once the node is booted, Digital Rebar automatically adds the node into the
system deployment. The system deployment is a special purpose deployment
used for discovery and base management. Users have limited options to
change it; however, the discovery process can be easily monitored by
watching the :ref:`ui_annealer` or :ref:`webui_deployment` screens. They will show
exactly which steps of the discovery progress are pending, acting and
completed.

A node is completely discovered when all the system deployment steps
(aka "node roles") are complete with green checks.

It is acceptable to configure nodes (the next steps) even before the
discovery is complete. Digital Rebar will figure out the correct order of
operations and perform actions in sequence.
