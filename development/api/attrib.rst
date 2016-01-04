Attribute (aka Attrib) APIs
~~~~~~~~~~~~~~~~~~~~~~~~~~~

Attribute APIs are used to manage attributes used by the jigs. Roles,
Nodes, NodeRoles, and DeploymentRoles all work with Attribs.

    To prevent Rails name collisions, Digital Rebar uses 'Attrib'
    instead of Attribute.

Routes
^^^^^^

+--------+-------------------------------------------------------------------+-----------+-----------------------------------------------------------------+------------+
| Verb   | URL                                                               | Options   | Returns                                                         | Comments   |
+========+===================================================================+===========+=================================================================+============+
| GET    | /api/v2/attribs                                                   | none      | List Attribs                                                    | -          |
+--------+-------------------------------------------------------------------+-----------+-----------------------------------------------------------------+------------+
| GET    | /api/v2/attribs/[:id]                                             | none      | Show Attrib                                                     | -          |
+--------+-------------------------------------------------------------------+-----------+-----------------------------------------------------------------+------------+
| GET    | /api/v2/nodes/[:node\_id]/attribs                                 | none      | List Attribs for a specific node                                | -          |
+--------+-------------------------------------------------------------------+-----------+-----------------------------------------------------------------+------------+
| GET    | /api/v2/nodes/[:node\_id]/attribs/[:id]                           | none      | Show Attrib (including value) for a specific Node               | -          |
+--------+-------------------------------------------------------------------+-----------+-----------------------------------------------------------------+------------+
| PUT    | /api/v2/nodes/[:node\_id]/attribs/[:id]                           | none      | Update Attrib                                                   | -          |
+--------+-------------------------------------------------------------------+-----------+-----------------------------------------------------------------+------------+
| GET    | /api/v2/roles/[:role\_id]/attribs                                 | none      | List Attribs for a specific role                                | -          |
+--------+-------------------------------------------------------------------+-----------+-----------------------------------------------------------------+------------+
| GET    | /api/v2/roles/[:role\_id]/attribs/[:id]                           | none      | Show Attrib (including value) for a specific Role               | -          |
+--------+-------------------------------------------------------------------+-----------+-----------------------------------------------------------------+------------+
| PUT    | /api/v2/roles/[:role\_id]/attribs/[:id]                           | none      | Update Attrib                                                   | -          |
+--------+-------------------------------------------------------------------+-----------+-----------------------------------------------------------------+------------+
| GET    | /api/v2/deployments/[:deployment\_id]/attribs                     | none      | List Attribs for a specific deployment                          | -          |
+--------+-------------------------------------------------------------------+-----------+-----------------------------------------------------------------+------------+
| GET    | /api/v2/deployments/[:deployment\_id]/attribs/[:id]               | none      | Show Attrib (including value) for a specific Deployment         | -          |
+--------+-------------------------------------------------------------------+-----------+-----------------------------------------------------------------+------------+
| PUT    | /api/v2/deployments/[:deployment\_id]/attribs/[:id]               | none      | Update Attrib                                                   | -          |
+--------+-------------------------------------------------------------------+-----------+-----------------------------------------------------------------+------------+
| GET    | /api/v2/deployment\_roles/[:deployment\_role\_id]/attribs         | none      | List Attribs for a specific deployment\_role                    | -          |
+--------+-------------------------------------------------------------------+-----------+-----------------------------------------------------------------+------------+
| GET    | /api/v2/deployment\_roles/[:deployment\_role\_id]/attribs/[:id]   | none      | Show Attrib (including value) for a specific Deployment\_Role   | -          |
+--------+-------------------------------------------------------------------+-----------+-----------------------------------------------------------------+------------+
| PUT    | /api/v2/deployment\_roles/[:deployment\_role\_id]/attribs/[:id]   | none      | Update Attrib                                                   | -          |
+--------+-------------------------------------------------------------------+-----------+-----------------------------------------------------------------+------------+
| GET    | /api/v2/node\_roles/[:node\_role\_id]/attribs                     | none      | List Attribs for a specific node\_role                          | -          |
+--------+-------------------------------------------------------------------+-----------+-----------------------------------------------------------------+------------+
| GET    | /api/v2/node\_roles/[:node\_role\_id]/attribs/[:id]               | none      | Show Attrib (including value) for a specific Node\_Role         | -          |
+--------+-------------------------------------------------------------------+-----------+-----------------------------------------------------------------+------------+
| PUT    | /api/v2/node\_roles/[:node\_role\_id]/attribs/[:id]               | none      | Update Attrib                                                   | -          |
+--------+-------------------------------------------------------------------+-----------+-----------------------------------------------------------------+------------+

List Attribs
^^^^^^^^^^^^

-  CLI: ``rebar attribs list``
-  API:
   ``curl -X GET         --digest -u $(cat /etc/rebar.install.key)         -H "Content-Type:application/json"         http://localhost:3000/api/v2/attribs``

Returns:

::

    [
      {
        "order": 10000,
        "barclamp_id": 2,
        "writable": false,
        "map": "ohai/dmi/base_board/asset_tag",
        "name": "asset_tag",
        "updated_at": "2014-03-03T05:18:01.883Z",
        "description": "BIOS configured system identifier",
        "id": 1,
        "role_id": null,
        "node_id": null,
        "schema": null,
        "created_at": "2014-03-03T05:18:01.873Z"
      },
      {
        "order": 10000,
        "barclamp_id": 2,
        "writable": false,
        "map": "ohai/dmi/base_board/asset_tag",
        "name": "serial_number",
        "updated_at": "2014-03-03T05:18:01.909Z",
        "description": "System Serial Number",
        "id": 2,
        "role_id": null,
        "node_id": null,
        "schema": null,
        "created_at": "2014-03-03T05:18:01.899Z"
      },
      ...
    ]

Show Attrib
^^^^^^^^^^^

-  CLI: ``rebar attribs show hint-admin-macs``
-  API:
   ``curl -X GET         --digest -u $(cat /etc/rebar.install.key)         -H "Content-Type:application/json"         http://localhost:3000/api/v2/attribs/hint-admin/macs``

Returns

::

    {
      "writable": true,
      "map": "admin_macs",
      "created_at": "2014-03-03T05:18:02.241Z",
      "id": 14,
      "barclamp_id": 2,
      "description": "Hint for Admin MAC addresses",
      "order": 10000,
      "updated_at": "2014-03-03T05:18:02.254Z",
      "name": "hint-admin-macs",
      "schema": {
        "type": "seq",
        "sequence": [
          {
            "type": "str",
            "pattern": "/([0-9a-fA-F]{2}:){5}[0-9a-fA-F]/"
          }
        ],
        "required": true
      },
      "role_id": null,
      "node_id": null
    }

