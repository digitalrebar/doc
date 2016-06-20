.. index::
  pair: Services; Forwarder
  pair: Container; Forwarder

.. _arch_service_forwarder:

Forwarder
---------

The forwarder container acts front to all other containers.  Other containers that are running in host mode are
switched to use this container as the networking component.  This container gets an address on the admin network
and the admin network must be bridged into the docker network.  This configuration is useful for development
when using KVM slaves to test provisioning and workloads.

This container is used when FORWARDER mode is specified in the deploy scripts or the docker-admin scripts.

