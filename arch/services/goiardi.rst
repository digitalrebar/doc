
.. note:: WARNING WARNING WARNING:  This is the Digital Rebar v2 product documentation.  The v2 version is EOL as of September 2017.  Please refer to the new Digital Rebar Provision v3 documentation:  http:\/\/provision.readthedocs.io\/en\/tip\/README.html

.. index::
  pair: Services; Goiardi
  pair: Services; Chef
  pair: Container; Goiardi

.. _arch_service_goiardi:

Goiardi
-------

The goiardi container runs a go-based Chef server replacement.  The system provides basic Chef server
functionality and is configured by the :ref:`arch_service_rebar_api` container upon start-up with cookbooks and roles to use
on nodes.  The Rebar API uses the :ref:`chef_jig` to manage client entries and run lists for those clients in the
goiardi server.
