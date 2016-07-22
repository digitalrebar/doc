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
