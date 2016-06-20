.. index::
  pair: Services; Rebar API
  pair: Services; Rebar Runner
  pair: Container; Rebar API

.. _arch_service_rebar_api:

Rebar API
---------

The Rebar API container runs the core application that is the brains of the system.  The application
provides the RestFUL Api for the :ref:`arch_objects` and the basic UI.

Within the container, the job runners execute as well.  These use the database to handle :ref:`object_node_role`
execution.

This container also registers with the :ref:`arch_service_revproxy` container to handle all non-handled requests.


