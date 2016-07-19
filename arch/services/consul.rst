.. index::
  pair: Services; Consul
  pair: Container; Consul

.. _arch_service_consul:

Consul
------

The consul container runs a recent version of consul without the UI.  It acts as the primary Key/Value
store for the system.  All other services register their presence and, in most cases, additional 
key/values that allow access, port information, or public identity information.

This container runs as a host container on the Admin node.
