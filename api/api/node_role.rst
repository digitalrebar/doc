
.. note:: WARNING WARNING WARNING:  This is the Digital Rebar v2 product documentation.  The v2 version is EOL as of September 2017.  Please refer to the new Digital Rebar Provision v3 documentation:  http:\/\/provision.readthedocs.io\/en\/tip\/README.html

.. index::
  pair: Node Role; API

.. _api_node_role:

Node Role APIs
~~~~~~~~~~~~~~

Node Roles are the core of Digital Rebar deployment and orchestration
engine

There are four types of data that Digital Rebar tracks while three 
are maintained on related NodeRoleDatum mode.

1. user data (node\_role.data) is set by users during the proposed state
   (also known as "out bound data")
2. system data (node\_role.sysdata) is set by rebar before annealing
   (also known as "out bound data")
3. wall data (node\_role.wall) is set by the jig after transition (also
   known as "in bound data")
4. discovery data (node.wall) is stored on the node instead of in node role
   because it reflects node information aggregated from all the jigs.
   This information is available using the node.attrib\_[name] and
   Attrib model.  Please see the node API docs for more about this type
   of data

NodeRole does not have a natural key, so they must be referenced by
ID or under the relevant Nodes, Roles, or Deployment.

API Actions
^^^^^^^^^^^

+----------+-------------------------------------------------------+-----------------------------------------------------------+
| Verb     | URL                                                   | Comments                                                  |
+==========+=======================================================+===========================================================+
| GET      | api/v2/node\_roles                                    | List                                                      |
+----------+-------------------------------------------------------+-----------------------------------------------------------+
| GET      | api/v2/node\_roles/:id                                | Specific Item                                             |
+----------+-------------------------------------------------------+-----------------------------------------------------------+
| PUT      | api/v2/node\_roles/:id                                | Update Item                                               |
+----------+-------------------------------------------------------+-----------------------------------------------------------+
| PUT      | api/v2/node\_roles/:id/retry                          | Retry (sets state back to TODO)                           |
+----------+-------------------------------------------------------+-----------------------------------------------------------+
| PUT      | api/v2/node\_roles/:id/propose                        | Propose (sets state to PROPOSED)                          |
+----------+-------------------------------------------------------+-----------------------------------------------------------+
| PUT      | api/v2/node\_roles/:id/commit                         | Commit (sets state to COMMIT)                             |
+----------+-------------------------------------------------------+-----------------------------------------------------------+
| POST     | api/v2/node\_roles                                    | Create Item                                               |
+----------+-------------------------------------------------------+-----------------------------------------------------------+
| GET      | /api/v2/node\_roles/[:node\_role\_id]/parents         | List Parent Node Roles (READ ONLY)                        |
+----------+-------------------------------------------------------+-----------------------------------------------------------+
| GET      | /api/v2/node\_roles/[:node\_role\_id]/children        | List Child Node Roles (READ ONLY)                         |
+----------+-------------------------------------------------------+-----------------------------------------------------------+
| GET      | /api/v2/node\_roles/[:node\_role\_id]/attribs         | List Attribs for a specific node\_role                    |
+----------+-------------------------------------------------------+-----------------------------------------------------------+
| GET      | /api/v2/node\_roles/[:node\_role\_id]/attribs/[:id]   | Show Attrib (including value) for a specific Node\_Role   |
+----------+-------------------------------------------------------+-----------------------------------------------------------+
| PUT      | /api/v2/node\_roles/[:node\_role\_id]/attribs/[:id]   | Update Attrib                                             |
+----------+-------------------------------------------------------+-----------------------------------------------------------+
| DELETE   | api/v2/node\_roles/:id                                | Allowed if Node Role does not have child dependencies     |
+----------+-------------------------------------------------------+-----------------------------------------------------------+

Helpers have been added to NodeRole create so that IDs are unnecessary when creating a new NodeRole. 
The following can be passed:

-  Deployment Name instead of Deployment ID
-  Node Name instead of Node ID
-  Role Name instead of Role ID

JSON fields
-----------

+------------------+----------------+------------+-------------------------+
| Attribute        | Type           | Settable   | Note                    |
+==================+================+============+=========================+
| Available        | Boolean        | Yes        |                         |
+------------------+----------------+------------+-------------------------+
| Cohort           | Integer        | ??         |                         |
+------------------+----------------+------------+-------------------------+
| Created\_at      | String         | No         | Unicode - date format   |
+------------------+----------------+------------+-------------------------+
| Updated\_at      | String         | No         | Unicode - date format   |
+------------------+----------------+------------+-------------------------+
| Runlog           | String         | ??         |                         |
+------------------+----------------+------------+-------------------------+
| Order            | Integer        | ??         |                         |
+------------------+----------------+------------+-------------------------+
| State            | Integer        | ??         |                         |
+------------------+----------------+------------+-------------------------+
| Node\_Error      | Boolean        | No         | Calculated              |
+------------------+----------------+------------+-------------------------+
| Node\_Id         | Integer        | Yes        |                         |
+------------------+----------------+------------+-------------------------+
| Status           | ??             | ??         |                         |
+------------------+----------------+------------+-------------------------+
| Run\_count       | Integer        | No         |                         |
+------------------+----------------+------------+-------------------------+
| Deployment\_Id   | Integer        | ??         |                         |
+------------------+----------------+------------+-------------------------+
| Role\_Id         | Integer        | Yes        |                         |
+------------------+----------------+------------+-------------------------+
| Id               | Internal Ref   | ??         | Actually an Int         |
+------------------+----------------+------------+-------------------------+

Field Notes
-----------

Node\_Error
~~~~~~~~~~~

*Calculated*

True if any of the NodeRoles on the associated Node are in an error
state.  This allows API users to monitor the status of a target role and
know if there was an error that will block progress without having to
inspect other NodeRoles.  Instead of looking at all parents (which could
span nodes), Node provides a more limited scope.
