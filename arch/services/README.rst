

.. index::
  Services; Overview
.. _arch_services:

Services
--------

Digital Rebar is composed of services.  These services are run in containers.  Most containers provide a single service that is exposed through consul.  The other services use consul connect and interact with each other.  Some services are exposed to the user or nodes.

.. toctree::
  :maxdepth: 2
  :glob:

  containers
  *
