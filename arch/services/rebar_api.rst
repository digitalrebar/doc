.. index::
  pair: Services; Rebar API
  pair: Services; Rebar Runner
  pair: Container; Rebar API

.. _arch_service_rebar_api:

Rebar API
---------

The Rebar API container runs the core application that is the brains of the system.  The application
provides the RestFUL API for the :ref:`arch_objects` and the basic UI (see :ref:`web_user_guide`).

Within the container, the job runners execute as well.  These use the database to handle object node role
execution.

This container also registers with the :ref:`arch_service_revproxy` container to handle all non-handled requests.

For more on the Rebar API, see :ref:`digital_rebar_api`.
