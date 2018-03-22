
.. note:: WARNING WARNING WARNING:  This is the Digital Rebar v2 product documentation.  The v2 version is EOL as of September 2017.  Please refer to the new Digital Rebar Provision v3 documentation:  http:\/\/provision.readthedocs.io\/en\/tip\/README.html

.. index::
	Digital Rebar; Using CURL

Using CURL with Digital Rebar
=============================

The Basics
----------

For any request, you will need to include the `digest` credentials as `user:password`.  Unless you've created a trusted certificate or installed the generated certificate, you'll also need to include `insecure`.

::

  curl --insecure --digest -u "rebar:rebar1"


GET
---

The most basic request is a GET request.  These requests will return JSON results as defined by the :ref:`api_pattern`.

::

  curl --insecure --digest -u "rebar:rebar1" -X GET "$REBAR_ENDPOINT/api/v2/nodes"


POST
----

Posts are used to create new models by passing a JSON request into the API endpoint.  They return 200 plus the JSON of created object like a GET if successful.  

> The headers are required.

::

  curl --insecure --digest -u "rebar:rebar1" -X POST -H "Accept: application/json" -H "Content-Type: application/json" -d '{"name":"foo"}' "$REBAR_ENDPOINT/api/v2/nodes"

