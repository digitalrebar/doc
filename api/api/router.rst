Router API
~~~~~~~~~~

The Router API is used to manage networks. It must be a child of a
specific network. There can be only one router per network.

Router CRUD
^^^^^^^^^^^

Lists the current ranges for a network.

**Input:**

+----------+--------------------------------------------------------------+----------------------------------------+----------------------------------------+------------+
| Verb     | URL                                                          | Options                                | Returns                                | Comments   |
+==========+==============================================================+========================================+========================================+============+
| GET      | network/api/v2/networks/[network]/network\_routers           | N/A                                    | JSON array of router for the network   |            |
+----------+--------------------------------------------------------------+----------------------------------------+----------------------------------------+------------+
| GET      | network/api/v2/network\_routers                              | N/A                                    | JSON array of routers                  |            |
+----------+--------------------------------------------------------------+----------------------------------------+----------------------------------------+------------+
| GET      | network/api/v2/networks/[network]/network\_routers/[any]     |                                        | Details of the router in JSON format   |            |
+----------+--------------------------------------------------------------+----------------------------------------+----------------------------------------+------------+
| GET      | network/api/v2/network\_routers/[id]                         | no natural key, requires Database ID   | Details of the router in JSON format   |            |
+----------+--------------------------------------------------------------+----------------------------------------+----------------------------------------+------------+
| POST     | network/api/v2/networks/[network]/network\_routers           | json definition                        | network id is infered from path        |            |
+----------+--------------------------------------------------------------+----------------------------------------+----------------------------------------+------------+
| POST     | network/api/v2/network\_routers                              | json definition                        | must include network id                |            |
+----------+--------------------------------------------------------------+----------------------------------------+----------------------------------------+------------+
| PUT      | network/api/v2/networks/[network]/network\_routers/[range]   |                                        | network id can be infered from path    |            |
+----------+--------------------------------------------------------------+----------------------------------------+----------------------------------------+------------+
| PUT      | network/api/v2/network\_routers/[range]                      |                                        |                                        |            |
+----------+--------------------------------------------------------------+----------------------------------------+----------------------------------------+------------+
| DELETE   | network/api/v2/networks/[network]/network\_routers/[range]   |                                        |                                        |            |
+----------+--------------------------------------------------------------+----------------------------------------+----------------------------------------+------------+
| DELETE   | network/api/v2/network\_routers/[range]                      |                                        |                                        |            |
+----------+--------------------------------------------------------------+----------------------------------------+----------------------------------------+------------+

Notes
^^^^^

-  Because only one router is allowed per network, Rebar ignores the ID
   of the router when used with the networks path.
-  Router does not conform to other Rebar object maps. It does not have
   a name, description or order.

