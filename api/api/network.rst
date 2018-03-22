
.. note:: WARNING WARNING WARNING:  This is the Digital Rebar v2 product documentation.  The v2 version is EOL as of September 2017.  Please refer to the new Digital Rebar Provision v3 documentation:  http:\/\/provision.readthedocs.io\/en\/tip\/README.html

.. index::
  pair: Network; API

.. _api_network:

Network API
~~~~~~~~~~~

The network API is used to manage networks.

Network CRUD
^^^^^^^^^^^^

Lists the current networks.

**Input:**

+----------+-----------------------------+-----------------------------------+-----------------------------------------+------------+
| Verb     | URL                         | Options                           | Returns                                 | Comments   |
+==========+=============================+===================================+=========================================+============+
| GET      | api/v2/networks             | N/A                               | JSON array of network IDs               |            |
+----------+-----------------------------+-----------------------------------+-----------------------------------------+------------+
| GET      | /v2/networks/[network]      | id is the network ID or name.     | Details of the network in JSON format   | -          |
+----------+-----------------------------+-----------------------------------+-----------------------------------------+------------+
| POST     | api/v2/networks             | json definition (see Node Show)   | must be a legal object                  |            |
+----------+-----------------------------+-----------------------------------+-----------------------------------------+------------+
| PUT      | api/v2/networks/[network]   |                                   |                                         |            |
+----------+-----------------------------+-----------------------------------+-----------------------------------------+------------+
| DELETE   | api/v2/networks/[network]   | Database ID or name               | HTTP error code 200 on success          |            |
+----------+-----------------------------+-----------------------------------+-----------------------------------------+------------+

    There are helpers on the POST method that allow the creation of ranges
    and routers when the network is created.

Sample:

::

    {
      "name":       "networkname",
      "deployment": "deploymentname",
      "vlan":       intended_vlan,
      "use_vlan":   true or false,
      "team_mode":  teaming mode,
      "use_team":   true or false,
      "use_bridge": true or false,
      "category":   "String to indicate type: admin,bmc,general,...",
      "group":      "String to indicate groups of networks",
      "conduit":    "1g0,1g1", // or whatever is desired as a conduit for this network
      "ranges": [
         { "name": "name", "first": "192.168.124.10/24", "last": "192.168.124.245/24" }
      ],
      "router": {
         "pref": 255, // or whatever pref is desired.  Lowest on a host will win.
         "address": "192.168.124.1/24"
      }
    }

Network Actions: IP Allocate
^^^^^^^^^^^^^^^^^^^^^^^^^^^^

Allocates a free IP address in a network.

+--------+-------------------------------------+-----------------------------------------------+----------------------------------+------------+
| Verb   | URL                                 | Options                                       | Returns                          | Comments   |
+========+=====================================+===============================================+==================================+============+
| POST   | api/v2/networks/[id]/allocate\_ip   | Database ID or name of the network barclamp   | HTTP error code 200 on success   |            |
+--------+-------------------------------------+-----------------------------------------------+----------------------------------+------------+

Network Actions: IP Deallocate
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

Deallocates a used IP address in a network.

+----------+-----------------------------------------------------------+-----------------------------------------------------------------------------------------------------------------------+----------------------------------+------------+
| Verb     | URL                                                       | Options                                                                                                               | Returns                          | Comments   |
+==========+===========================================================+=======================================================================================================================+==================================+============+
| DELETE   | api/v2/networks/deallocate\_ip/[network\_id]/[node\_id]   | id: Database ID or name of proposalnetwork\_id: Database ID or name of networknode\_id: Database ID or name of node   | HTTP error code 200 on success   |            |
+----------+-----------------------------------------------------------+-----------------------------------------------------------------------------------------------------------------------+----------------------------------+------------+

