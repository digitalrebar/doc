.. index::
  pair: Services; Goiardi
  pair: Services; Chef
  pair: Container; Goiardi

.. _arch_service_goiardi:

Goiardi
-------

The goiardi container runs a go-based chef server replacement.  The system provides the basic Chef server
functionality and is configured by the Rebar API container on start-up with cookbooks and roles to use
on nodes.  The Rebar API uses the Chef Jig to manage client entries and run lists for those clients in the
goiardi server.

