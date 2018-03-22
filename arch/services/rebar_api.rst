
.. note:: WARNING WARNING WARNING:  This is the Digital Rebar v2 product documentation.  The v2 version is EOL as of September 2017.  Please refer to the new Digital Rebar Provision v3 documentation:  http:\/\/provision.readthedocs.io\/en\/tip\/README.html

.. index::
  pair: Services; Rebar API
  pair: Services; Rebar Runner
  pair: Container; Rebar API

.. _arch_service_rebar_api:

Rebar API
---------

The Rebar API container runs the core application that is the brains of the system.  The application
provides the RestFUL API for the :ref:`arch_objects` and the basic UX (see :ref:`web_ux_guide`).

Within the container, the job runners execute as well.  These use the database to handle object node role
execution.

This container also registers with the :ref:`arch_service_revproxy` container to handle all non-handled requests.

For more on the Rebar API, see :ref:`digital_rebar_api`.
