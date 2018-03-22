
.. note:: WARNING WARNING WARNING:  This is the Digital Rebar v2 product documentation.  The v2 version is EOL as of September 2017.  Please refer to the new Digital Rebar Provision v3 documentation:  http:\/\/provision.readthedocs.io\/en\/tip\/README.html

.. index::
  pair: Services; Logging
  pair: Container; Logging

.. _arch_service_logging:

Logging
-------

The logging container runs syslog message receiver.  During provisioning, the bare metal nodes are configured
to send logs to the :ref:`arch_other_systems`'s logging service.  The service is also configured after installation.
The logging service stores per-node log files.
