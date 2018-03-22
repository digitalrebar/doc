
.. note:: WARNING WARNING WARNING:  This is the Digital Rebar v2 product documentation.  The v2 version is EOL as of September 2017.  Please refer to the new Digital Rebar Provision v3 documentation:  http:\/\/provision.readthedocs.io\/en\/tip\/README.html

.. index::
  pair: Interface; API

.. _api_interface:

Interface (NICs) API
~~~~~~~~~~~~~~~~~~~~

The Interface API is used to update the Node -> NIC Bus mapping

Lists the current networks.

**Input:**

+--------+---------------------------------+-----------+------------------------------------+-------------------+
| Verb   | URL                             | Options   | Returns                            | Comments          |
+========+=================================+===========+====================================+===================+
| GET    | api/v2/interfaces               | N/A       | JSON array of Interface Mappings   |                   |
+--------+---------------------------------+-----------+------------------------------------+-------------------+
| POST   | api/v2/interfaces               | -         | -                                  | Add new mapping   |
+--------+---------------------------------+-----------+------------------------------------+-------------------+
| PUT    | api/v2/interfaces/[Node Type]   |           |                                    |                   |
+--------+---------------------------------+-----------+------------------------------------+-------------------+

Data:

For POST/PUT use the following

::

    JSON ={"pattern"=>"node type", "bus_order"=>"0000:00/0000:00:01 | 0000:00/0000:00:03 | etc"}=

Notes:

-  There is no DELETE method.
-  These changes are made to the System DeploymentRole Data for the
   "network-server" role

