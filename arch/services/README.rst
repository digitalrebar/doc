
.. note:: WARNING WARNING WARNING:  This is the Digital Rebar v2 product documentation.  That product line is EOL as of September 2017.  Please refer to the new Digital Rebar Provision v3 documentation:  http:\/\/provision.readthedocs.io\/en\/tip\/README.html



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
