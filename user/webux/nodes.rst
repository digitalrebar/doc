
.. note:: WARNING WARNING WARNING:  This is the Digital Rebar v2 product documentation.  The v2 version is EOL as of September 2017.  Please refer to the new Digital Rebar Provision v3 documentation:  http:\/\/provision.readthedocs.io\/en\/tip\/README.html

.. _ux_nodes:

Nodes
=====


Nodes are a core element of the Digital Rebar system. From the "Nodes" page all the nodes in a deployment are visible, and display their addresses, descriptions, providers, developments, and tenants. 


.. image:: /images/screens/webux/nodes.png

Adding Nodes
************

To add a node, click the plus icon in the bottom right hand corner of the screen. 

.. image:: /images/icons/UX/add_icon.png

This will pull up a box to set the name, provider, deployment, and profiles that the node will belong to.  It also allows for multiple nodes to be made.

.. image:: /images/icons/UX/add_node.png

Node States
************

Digital Rebar does not maintain a single node state; instead, state is composed from the node roles that are assigned to the node.

As a convenience, these states are summarized for users:

  * If all states are ready, then the node is considered ready.
  * If any are error, then the node is considered in error.
  * If any are proposed, then the node is considered proposed.
  * Any other state, then the node is considered in transition.

Nodes have several override conditions that prevent Digital Rebar from operating on them.  These conditions are powered-off and reserved.  If these states are true, Digital Rebar will not attempt to use the node.

Cloud Nodes
-----------

Digital Rebar can create/destroy nodes on external "cloud" systems using the :ref:`ux_providers` system.

