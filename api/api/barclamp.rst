
.. note:: WARNING WARNING WARNING:  This is the Digital Rebar v2 product documentation.  That product line is EOL as of September 2017.  Please refer to the new Digital Rebar Provision v3 documentation:  http:\/\/provision.readthedocs.io\/en\/tip\/README.html

.. index::
  pair: Barclamp; API

.. _api_barclamp:

Barclamp APIs
~~~~~~~~~~~~~

Barclamps are the core modulization for Digital Rebar.  For that reason,
the API for barclamps is more limited because changes to barclamps can
cause breaking changes to the framework.

Routes
^^^^^^

+--------+---------------------------+-----------+------------------+------------+
| Verb   | URL                       | Options   | Returns          | Comments   |
+========+===========================+===========+==================+============+
| GET    | /api/v2/barclamps/        | none      | List Barclamps   | -          |
+--------+---------------------------+-----------+------------------+------------+
| GET    | /api/v2/barclamps/[:id]   | none      | Show Barclamp    | -          |
+--------+---------------------------+-----------+------------------+------------+

List Barclamps
^^^^^^^^^^^^^^

-  CLI: ``rebar barclamps list``
-  API:
   ``curl -X GET         --insecure --digest -u 'rebar:rebar1'         -H "Content-Type:application/json"         https://localhost/api/v2/barclamps``

Returns:

::

    [
      {
        "name": "core",
        "source_url": "https://github.com/digitalrebar/digitalrebar/core",
        "created_at": "2014-03-03T05:18:01.330Z",
        "id": 1,
        "source_path": "/opt/digitalrebar/core",
        "description": "Core",
        "commit": "unknown",
        "barclamp_id": 1,
        "version": 2,
        "build_on": null,
        "updated_at": "2014-03-03T05:18:01.400Z"
      },
      {
        "name": "rebar",
        "source_url": "http://github/digitalrebar/digitalrebar/unknown",
        "created_at": "2014-03-03T05:18:01.709Z",
        "id": 2,
        "source_path": "/opt/digitalrebar/core",
        "description": "Rebar",
        "commit": "unknown",
        "barclamp_id": 2,
        "version": 2,
        "build_on": null,
        "updated_at": "2014-03-03T05:18:01.737Z"
      },
      ...
    ]

Show Barclamp
^^^^^^^^^^^^^

-  CLI: ``rebar barclamps show core``
-  API:
   ``curl -X GET         --insecure --digest -u 'rebar:rebar1'         -H "Content-Type:application/json"         https://localhost/api/v2/barclamps/core``

Returns:

::

    {
      "commit": "unknown",
      "build_on": null,
      "updated_at": "2014-03-03T05:18:01.400Z",
      "description": "Core",
      "barclamp_id": 1,
      "version": 2,
      "source_url": "https://github.com/digitalrebar/core",
      "source_path": "/opt/digitalrebar/core",
      "created_at": "2014-03-03T05:18:01.330Z",
      "id": 1,
      "name": "core"
    }

