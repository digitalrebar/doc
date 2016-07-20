.. index::
  pair: Network Range; API

.. _api_network_range:

Range API
~~~~~~~~~

The Range API is used to manage networks. It must be a child of a
specific network.

Range CRUD
^^^^^^^^^^

Lists the current ranges for a network.

**Input:**

+--------+----------------------------------------------------+-----------------------------------+-----------------------------------------+------------+
| Verb   | URL                                                | Options                           | Returns                                 | Comments   |
+========+====================================================+===================================+=========================================+============+
| GET    | network/api/v2/networks/[network]/ranges           | N/A                               | JSON array of ranges                    |            |
+--------+----------------------------------------------------+-----------------------------------+-----------------------------------------+------------+
| GET    | network/api/v2/networks/[network]/ranges/[range]   |                                   | Details of the network in JSON format   |            |
+--------+----------------------------------------------------+-----------------------------------+-----------------------------------------+------------+
| POST   | network/api/v2/networks/[network]/ranges           | json definition (see Node Show)   | must be a legal object                  |            |
+--------+----------------------------------------------------+-----------------------------------+-----------------------------------------+------------+
| PUT    | network/api/v2/networks/[network]/ranges/[range]   |                                   |                                         |            |
+--------+----------------------------------------------------+-----------------------------------+-----------------------------------------+------------+

A range cannot be deleted at this time, the entire network must be destroyed in order to delete a range. 