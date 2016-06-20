.. index::
  pair: Services; Postgres
  pair: Container; Postgres

.. _arch_service_postgres:

Postgres
--------

The postgres container runs the database for the entire system.  The Rebar API and Goiardi containers each
have a database in this postgres instance.  The postgres stores the data in a mounted volume from the host.
The default directory is the deploy/compose/data-dir/postgres.

