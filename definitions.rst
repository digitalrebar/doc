
.. note:: WARNING WARNING WARNING:  This is the Digital Rebar v2 product documentation.  The v2 version is EOL as of September 2017.  Please refer to the new Digital Rebar Provision v3 documentation:  http:\/\/provision.readthedocs.io\/en\/tip\/README.html

.. index::
  Definitions

.. _definitions:

Definitions
-----------

+-------------------+-------------------------------------------------------------------------------------+
+ Term              | Definition                                                                          |
+===================+=====================================================================================+
+ Admin Node        | System running the containers needed for Digital Rebar.  Can be VM or Physical      |
+-------------------+-------------------------------------------------------------------------------------+
+ Anneal            | The method of processing unrun Node Roles on Nodes.                                 |
+-------------------+-------------------------------------------------------------------------------------+
+ Bare Metal Node   | Any physical node managed by Digital Rebar.                                         |
+-------------------+-------------------------------------------------------------------------------------+
+ Managed Node      | Any node that is managed by Digital Rebar.  Can be VM or Physical                   |
+-------------------+-------------------------------------------------------------------------------------+
| Node              | A VM or physical system that Digital Rebar may manage or is managing.  It is        |
|                   | represented by an object node.                                                      |
+-------------------+-------------------------------------------------------------------------------------+
| Node Role         | An instance of a role on a specific node.  These are sequenced into a directed      |
|                   | graph and annealed to completion.                                                   |
+-------------------+-------------------------------------------------------------------------------------+
| Role              | An atomic piece of functionality to apply to a node. :ref:`object_role`             |
+-------------------+-------------------------------------------------------------------------------------+
| Sledgehammer      | A RAM-only boot environment served by the provisioner for bare metal node discovery |
+-------------------+-------------------------------------------------------------------------------------+


