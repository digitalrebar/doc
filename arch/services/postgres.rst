
.. note:: WARNING WARNING WARNING:  This is the Digital Rebar v2 product documentation.  That product line is EOL as of September 2017.  Please refer to the new Digital Rebar Provision v3 documentation:  http:\/\/provision.readthedocs.io\/en\/tip\/README.html

.. index::
  pair: Services; Postgres
  pair: Container; Postgres

.. _arch_service_postgres:

Postgres
--------

The postgres container runs the database for the entire system.  The :ref:`arch_service_rebar_api` and :ref:`arch_service_goiardi` containers each
have a database in this postgres instance.  The postgres stores the data in a mounted volume from the host.
Its default directory is ``deploy/compose/data-dir/postgres``.
