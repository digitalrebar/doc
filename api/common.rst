.. index::
  pair: API; Reference Guide

.. _api_info:

Common Information about the Digital Rebar API
----------------------------------------------

This document is the reference guide for the Digital Rebar API.

Our intention is to keep the API documentation focused just on using
the API and leave more to curious readers to review the model and
principles areas.


Using the API
~~~~~~~~~~~~~

The Digital Rebar API is RESTful and accepts/returns JSON.  XML output is
not supported.

The Digital Rebar API is versioned.  API urls include the Digital Rebar
version of the API (e.g.: 1.0 or v2).  Please use the most recent version
available!

Legacy Note: routes with 1.0 are deprecated!

.. index::
  pair: API; Behavior Pattern

.. _api_pattern:

Digital Rebar API Pattern
~~~~~~~~~~~~~~~~~~~~~~~~~

The Digital Rebar API sticks to the following behavior patterns.

Expectations:
^^^^^^^^^^^^^

-  Core objects can be referenced equally by name or ID.  This means that
   objects with natural key names are NOT allowed to start with a number
   (similar to FQDN restrictions)
-  JSON is the API serialization model

Digest Authentication
^^^^^^^^^^^^^^^^^^^^^

API callers use digest authentication for all requests.  User accounts
need to be specifically configured for API only access.  A user account
with API access will still be able to log in normally.

To get the digest, make a HEAD or GET request to /api/v2/digest

.. index::
  API; URL Patterns

Common API URL Patterns:
^^^^^^^^^^^^^^^^^^^^^^^^

Digital Rebar uses a versioned URL pattern.  By convention, resource
names are pluralized in the API.  For example, the API will use ``nodes``
instead of ``node`` in paths.

-  Base Form: ``[workload | api]/[version]/[resources]/[id]``
-  Version: version of Digital Rebar framework being used (v2 for this
   guide)
-  Workload: Workload (aka :ref:`ui_barclamps`) that owns the requested activity.
   Framework uses 'api'
-  bc\_version: the version of the barclamp being used.
-  key\_word: groups the API into different categories

   -  reserved words such as status and rebar
   -  resource types like node, group, network, etc

-  id: (optional) Name or DB id of the barclamp configuration
-  Result codes:

   -  200 = OK, success
   -  500 = Error in processing.
   -  404 = item not found in database (may return 500 in some cases)

-  List:

   -  HTTP get
   -  Returns a JSON array of objects

-  CRUD Operations:

   -  id: name or database ID of the item.  Items that do not have natural keys are not expected to honor use of name instead of database ID.  When possible, either will be allowed.

-  RESTful Verbs for CRUD:

   -  POST / Create: ID is ignored if provided
   -  GET / Read: Objects will be shallow
   -  PUT / Update: returns the updated object serialized
   -  DELETE/ Delete: no return data except 200

-  Special Cases

   -  PUT: used to start an action on existing data (commit a node or
      deployment)
   -  DELETE: Unlink/Deactivate/Dequeue

In general, Digital Rebar REST pattern uses the 4 HTTP verbs as follows:

-  GET to retrieve information
-  PUT to transform or change existing data
-  POST to create new data or relationships
-  DELETE to remove data or relationships

.. index::
  pair: API; Expected Fields

Expected Fields
~~~~~~~~~~~~~~~

By convention, most Digital Rebar models have the same fields:

-  id: database assigned role, number
-  name: resource name, often a natural key with enforced uniqueness
-  description: user definable content
-  created\_at: when object was created
-  updated\_at: when object was last updated
-  object\_id: cross reference id to an object.  In most cases, the name
   of the object can be used instead of the API

    Some of the information stored in objects is maintained as json and
    will appear as nested data.

.. index::
  API; Headers and Response Patterns

API Headers & Response Patterns
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

The Digital Rebar REST API uses HTTP ``content-type`` metadata header
tags to help clients quickly identify the information being returned by
the API.

The API adds ="application/vnd.rebar.[type].[form]+json;version=2.0"= to
the content-type tag.

If only certain attributes need to be returned for an API
call, the ``x-return-attributes`` header can be to a JSON array of
the attributes that need to be returned.

-  [type] is the object type being returned.  E.g.: node, deployment,
   jig, etc
-  [form] describes how the objects are formed
-  obj = single obj
-  list = list of objects
-  empty = nothing
-  error = error.

REST results should be returned with the appropriate standard HTTP
response code, such as:

-  200 = ok
-  404 = object not found
-  500 = application error
-  `complete
   list <http://en.wikipedia.org/wiki/List_of_HTTP_status_codes>`__

Example Documentation
~~~~~~~~~~~~~~~~~~~~~

.. index::
  pair: API; Actions

API Actions
^^^^^^^^^^^

+-----------+------------------------------+-----------------+
| Verb      | URL                          | Comments        |
+===========+==============================+=================+
| GET       | api/v2/resources             | List            |
+-----------+------------------------------+-----------------+
| GET       | api/v2/resources/:id         | Specific Item   |
+-----------+------------------------------+-----------------+
| PUT       | api/v2/resources/:id         | Update Item     |
+-----------+------------------------------+-----------------+
| POST      | api/v2/resources             | Create Item     |
+-----------+------------------------------+-----------------+
| DELETE    | api/v2/resources/:id         | Delete Item     |
+-----------+------------------------------+-----------------+
| VARIOUS   | api/v2/resources/:id/extra   | Special Ops     |
+-----------+------------------------------+-----------------+

JSON Output Example:
~~~~~~~~~~~~~~~~~~~~

::

    {
      "id":41,
      "name":"sim.cr0wbar.com",
      "description":"example",
      "order":100,
      "admin":true,
      "alive":true,
      "allocated":false,
      "available":true,
      "bootenv":"sledgehammer",
      "deployment_id":1,
      "discovery":{
         {"foo":"this is json"}
      },
      "created_at":"2013-11-01T03:23:27Z",
      "updated_at":"2013-11-01T03:23:27Z"
    }

Some workflow examples (using the Rebar CLI)
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

Creating a Node for a system that already has an OS:
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

This example will explain how to create a new node in Rebar for an
already-installed system that we want to bring under Rebar management.
This example assumes that it has a non-conflicting IP address that is
already in the nodes range of the admin network, that the public key of
the Rebar user will let the Script jig run things as root on the node,
and that there is already a Rebar-compatible operating system installed.

-  CLI::

    rebar nodes create '{"name": "newtest.cr0wbar.com", "bootenv": "local"}

-  API::

    curl --insecure --digest -u 'rebar:rebar1'
    -X POST
    -d "name=newtest.cr0wbar.com"
    -d "bootenv=local"
    -H "Content-Type:application/json"
    --url https://127.0.0.1/api/v2/nodes

This will return::

  { "admin":false, "alive":false, "allocated":false,
  "available":false, "bootenv":"local",
  "created\_at":"2013-12-21T05:49:00Z", "deployment\_id":1,
  "description":"", "discovery":{}, "hint":{}, "id":41,
  "name":"newtest.cr0wbar.com", "order":100, "target\_role\_id":null,
  "updated\_at":"2013-12-21T05:49:00Z" }

After creating the node, we still need to set the hint for the Admin IP
to have Rebar try and use the one it already has:

-  CLI::

    rebar nodes set newtest.cr0wbar.com attrib hint-admin-v4addr to '{"value": "192.168.124.99/24"}

-  API::

    curl --insecure --digest -u 'rebar:rebar1' -X PUT -H "Content-Type:application/json"  --url https://127.0.0.1/api/v2/nodes/newtest.cr0wbar.com/attribs/hint-admin-v4addr     -d '{"value": "192.168.124.99/24"}'

We then need to bind a useful set of default node roles to the node:

-  CLI::

    rebar roles bind rebar-managed-node to newtest.cr0wbar.com

-  API::

    curl --insecure --digest -u 'rebar:rebar1' -X POST -H "Content-Type:application/json" --url https://127.0.0.1/api/v2/node_roles     -d '{"node": "newtest.cr0wbar.com", "role": "rebar-managed-node"}'

Commit the node, which will move the newly-created node roles from
proposed to todo or blocked, and mark the node as available:

-  CLI: ``rebar nodes commit newtest.cr0wbar.com``
-  API:
   ``curl --insecure --digest -u 'rebar:rebar1'     -X PUT     -H "Content-Type:application/json"     --url https://127.0.0.1/api/v2/nodes/newtest.cr0wbar.com/commit``

Mark the node as alive, which will allow the Annealer to do its thing:

-  CLI::

    rebar nodes update newtest.cr0wbar.com '{"alive": true}'

-  API::

    curl --insecure --digest -u 'rebar:rebar1'     -X PUT     -H "Content-Type:application/json"     --url https://127.0.0.1/api/v2/nodes/newtest.cr0wbar.com     -d 'alive=true'

Installing an operating system on a node
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

Get the names of the nodes for install:
'''''''''''''''''''''''''''''''''''''''

-  CLI: ``rebar nodes list --attributes name``
-  API:
   ``curl --insecure --digest -u 'rebar:rebar1'     -X GET     -H "Content-Type:application/json"     -H 'x-return-attributes:["name"]'     --url https://127.0.0.1/api/v2/nodes``

Returns:

::

    [
      {
        "name": "78e3be198029.smoke.test"
      },
      {
        "name": "d52-54-05-3f-00-00.smoke.test"
      }
    ]

Create a deployment to deploy the nodes into:
'''''''''''''''''''''''''''''''''''''''''''''

-  CLI: ``rebar deployments create '{"name": "test1"}'``
-  API:
   ``curl --insecure --digest -u 'rebar:rebar1'     -X POST     -H "Content-Type:application/json"     --url https://127.0.0.1/api/v2/deployments     -d '{"name": "test1"}'``

Returns:

::

    {
      "system": false,
      "created_at": "2014-03-03T04:40:07.351Z",
      "state": 0
      "parent_id": 1,
      "description": null,
      "updated_at": "2014-03-03T04:40:07.351Z",
      "id": 2,
      "name": "test1"
    }

Update the target node with the new deployment that was just created:
'''''''''''''''''''''''''''''''''''''''''''''''''''''''''''''''''''''

-  CLI: ``rebar nodes move d52-54-05-3f-00-00.smoke.test to test1``
-  API:
   ``curl --insecure --digest -u 'rebar:rebar1'     -X PUT     -H "Content-Type:application/json"     --url https://127.0.0.1/api/v2/nodes/d52-54-05-3f-00-00.smoke.test     -d '{"deployment": "test1"}'``

Returns:

::

    {
      "description": null,
      "target_role_id": null,
      "deployment_id": 2,
      "alive": true,
      "hint": {
        "admin_macs": [
          "52:54:05:3f:00:00"
        ]
      },
      "bootenv": "sledgehammer",
      "admin": false,
      "created_at": "2014-03-03T04:35:19.642Z",
      "name": "d52-54-05-3f-00-00.smoke.test",
      "id": 2,
      "order": 10000,
      "discovery": {},
      "available": true,
      "allocated": false,
      "updated_at": "2014-03-03T04:41:13.342Z"
    }

Create a node-role to bind the role to the node:
''''''''''''''''''''''''''''''''''''''''''''''''

-  CLI:
   ``rebar roles bind rebar-installed-node to d52-54-05-3f-00-00.smoke.test``
-  API:
   ``curl --insecure --digest -u 'rebar:rebar1'     -X POST     -H "Content-Type:application/json"     --url https://127.0.0.1/api/v2/node_roles     -d '{"node": "d52-54-05-3f-00-00.smoke.test", "role": "rebar-installed-node"}'``

Returns:

::

    {
      "id": 25,
      "role_id": 3,
      "state": 4,
      "run_count": 0,
      "node_id": 2,
      "deployment_id": 2,
      "available": true,
      "runlog": "",
      "order": 10000,
      "created_at": "2014-03-03T04:47:43.856Z",
      "updated_at": "2014-03-03T04:47:43.860Z",
      "cohort": 10,
      "status": null
    }

(Optional) Change the operating system to deploy onto the node:
'''''''''''''''''''''''''''''''''''''''''''''''''''''''''''''''

-  CLI:
   ``rebar nodes set d52-54-05-3f-00-00.smoke.test attrib   provisioner-target_os to '{"value": "ubuntu-12.04"}'``
-  API:
   ``curl --insecure --digest -u 'rebar:rebar1'     -X PUT     -H "Content-Type:application/json"     --url https://127.0.0.1/api/v2/nodes/d52-54-05-3f-00-00.smoke.test/attribs/provisioner-target_os     -d '{"value": "ubuntu-12.04"}'``

Returns:

::

    {
      "updated_at": "2014-03-03T16:37:43.478Z",
      "description": "The operating system to install on a node",
      "writable": true,
      "barclamp_id": 7,
      "value": "ubuntu-12.04",
      "order": 10000,
      "name": "provisioner-target_os",
      "id": 37,
      "role_id": 24,
      "created_at": "2014-03-03T16:37:43.466Z",
      "schema": {
        "required": true,
        "enum": [
          "ubuntu-12.04",
          "redhat-6.5",
          "centos-6.6"
        ],
        "type": "str"
      },
      "map": "rebar/target_os"
    }

Commit the deployment:
''''''''''''''''''''''

-  CLI: ``rebar deployments commit test1``
-  API:
   ``curl --insecure --digest -u 'rebar:rebar1'     -X PUT     -H "Content-Type:application/json"     --url https://127.0.0.1/api/v2/deployments/test1/commit``

Returns:

::

    {
      "name": "test1",
      "system": false,
      "parent_id": 1,
      "id": 2,
      "created_at": "2014-03-03T04:40:07.351Z",
      "updated_at": "2014-03-03T04:40:07.351Z",
      "description": null
    }
