
.. note:: WARNING WARNING WARNING:  This is the Digital Rebar v2 product documentation.  The v2 version is EOL as of September 2017.  Please refer to the new Digital Rebar Provision v3 documentation:  http:\/\/provision.readthedocs.io\/en\/tip\/README.html

.. index::
  pair: Deployment Role; API

.. _api_deployment_role:

Deployment-Role API
~~~~~~~~~~~~~~~~~~~

DeploymentRoles provide the default values for node-roles in a
deployment.  They are populated from the role's template during import.

Unlike node-roles, they do not store any inbound or system data.

API Actions
^^^^^^^^^^^

+----------+-------------------------------------------------------------------+-----------------------------------------------------------------+
| Verb     | URL                                                               | Comments                                                        |
+==========+===================================================================+=================================================================+
| GET      | api/v2/deployment\_roles                                          | List                                                            |
+----------+-------------------------------------------------------------------+-----------------------------------------------------------------+
| GET      | api/v2/deployment\_roles/:id                                      | Specific Item                                                   |
+----------+-------------------------------------------------------------------+-----------------------------------------------------------------+
| PUT      | api/v2/deployment\_roles/:id                                      | Update Item                                                     |
+----------+-------------------------------------------------------------------+-----------------------------------------------------------------+
| POST     | api/v2/deployment\_roles                                          | Create Item                                                     |
+----------+-------------------------------------------------------------------+-----------------------------------------------------------------+
| GET      | /api/v2/deployment\_roles/[:deployment\_role\_id]/attribs         | List Attribs for a specific deployment\_role                    |
+----------+-------------------------------------------------------------------+-----------------------------------------------------------------+
| GET      | /api/v2/deployment\_roles/[:deployment\_role\_id]/attribs/[:id]   | Show Attrib (including value) for a specific Deployment\_Role   |
+----------+-------------------------------------------------------------------+-----------------------------------------------------------------+
| PUT      | /api/v2/deployment\_roles/[:deployment\_role\_id]/attribs/[:id]   | Update Attrib                                                   |
+----------+-------------------------------------------------------------------+-----------------------------------------------------------------+
| DELETE   | -                                                                 | NOT SUPPORTED                                                   |
+----------+-------------------------------------------------------------------+-----------------------------------------------------------------+

