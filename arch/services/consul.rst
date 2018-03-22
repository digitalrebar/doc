
.. note:: WARNING WARNING WARNING:  This is the Digital Rebar v2 product documentation.  The v2 version is EOL as of September 2017.  Please refer to the new Digital Rebar Provision v3 documentation:  http:\/\/provision.readthedocs.io\/en\/tip\/README.html

.. index::
  pair: Services; Consul
  pair: Container; Consul

.. _arch_service_consul:

Consul
------

The consul container runs a recent version of consul without the UI.  It acts as the primary Key/Value
store for the system.  All other services register their presence and, in most cases, additional
key/values that allow access, port information, or public identity information with the consul.

This container runs as a host container on the :ref:`arch_other_systems`.
