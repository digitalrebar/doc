
.. note:: WARNING WARNING WARNING:  This is the Digital Rebar v2 product documentation.  The v2 version is EOL as of September 2017.  Please refer to the new Digital Rebar Provision v3 documentation:  http:\/\/provision.readthedocs.io\/en\/tip\/README.html

.. index::
  pair: Capability; API

.. _api_capability:

Capability APIs
~~~~~~~~~~~~~~~

Capabilities Routes
^^^^^^^^^^^^^^^^^^^

+--------+-------------------------------------------------------+-----------+-----------------------------------------------------------+------------+
| Verb   | URL                                                   | Options   | Returns/Comments                                          | Nothing    |
+========+=======================================================+===========+===========================================================+============+
| GET    | /api/v2/capabilities                                  | none      | Capability List                                           | -          |
+--------+-------------------------------------------------------+-----------+-----------------------------------------------------------+------------+
| POST   | /api/v2/capabilities                                  | none      | New Capability                                            | -          |
+--------+-------------------------------------------------------+-----------+-----------------------------------------------------------+------------+
| GET    | /api/v2/capabilities/[:id]                            | none      | Existing Capability Detail                                | -          |
+--------+-------------------------------------------------------+-----------+-----------------------------------------------------------+------------+
| PUT    | /api/v2/capabilities/[:id]                            | none      | Update Capability Detail                                  | -          |
+--------+-------------------------------------------------------+-----------+-----------------------------------------------------------+------------+
| GET    | /api/v2/capabilities/[:id]                            | none      | Existing Capability Detail                                | -          |
+--------+-------------------------------------------------------+-----------+-----------------------------------------------------------+------------+


Source Field
------------

Capabilities include a "source" field that is internally managed and cannot set set by users.  When new capabities are created, they are always sourced as ``user-defined``.

Values for source include:

* user-defined: user created capabilities
* Rebar services depending on the services running, including:

	* provisioner
	* rebar-api
	* rebar-dhcp
	* rebar-dns

* cap-groups: contain all the capabilities starting with a prefix like "NODE-" and are helpful for defining admin rights.
* dr-groups: are system defined groups that should meet common needs


JSON fields
-----------

+---------------+----------------+------------+-----------------------------------------------------------+
| Attribute     | Type           | Settable   | Note                                                      |
+===============+================+============+===========================================================+
| Name          | String         | Yes        | Limited to UPPER Alpha & _ - no spaces or special chars   |
+---------------+----------------+------------+-----------------------------------------------------------+
| Description   | String         | Yes        |                                                           |
+---------------+----------------+------------+-----------------------------------------------------------+
| Source        | String         | No         | See Note above                                            |
+---------------+----------------+------------+-----------------------------------------------------------+
| Includes      | Array          | Yes        | Contains other capabilities                               |
+---------------+----------------+------------+-----------------------------------------------------------+
| Created\_at   | String         | No         | Unicode - date format                                     |
+---------------+----------------+------------+-----------------------------------------------------------+
| Updated\_at   | String         | No         | Unicode - date format                                     |
+---------------+----------------+------------+-----------------------------------------------------------+

Minimum fields needed for create - name
