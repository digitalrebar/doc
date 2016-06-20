.. index::
  Definitions

.. _defintions:

Definitions
-----------

+-------------------+-------------------------------------------------------------------------------------+
+ Term              | Definition                                                                          |
+===================+=====================================================================================+
+ Admin Node        | System running the containers needed for Digital Rebar.  Can be VM or Phyiscal      |
+-------------------+-------------------------------------------------------------------------------------+
+ Anneal            | The method of processing unrun Node Roles on Nodes.                                 |
+-------------------+-------------------------------------------------------------------------------------+
+ Bare Metal Node   | Any physical node managed by Digital Rebar.                                         |
+-------------------+-------------------------------------------------------------------------------------+
+ Managed Node      | Any node that is managed by Digital Rebar.  Can be VM or Physical                   |
+-------------------+-------------------------------------------------------------------------------------+
| Node              | A VM or physical system that Digital Rebar may manage or is managing.  It is        |
|                   | represented by a :ref:`object_node`.                                                |
+-------------------+-------------------------------------------------------------------------------------+
| Node Role         | An instance of a role on a specific node.  These are sequenced into a directed      |
|                   | graph and annealed to completion.                                                   |
+-------------------+-------------------------------------------------------------------------------------+
| Role              | An atomic piece of functionality to apply to a node. :ref:`object_role`             |
+-------------------+-------------------------------------------------------------------------------------+
| Sledgehammer      | A RAM-only boot environment served by the provisioner for bare metal node discovery |
+-------------------+-------------------------------------------------------------------------------------+


