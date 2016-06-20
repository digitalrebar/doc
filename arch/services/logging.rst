.. index::
  pair: Services; Logging
  pair: Container; Logging

.. _arch_service_logging:

Logging
-------

The logging container runs syslog message receiver.  During provisioning, the bare metal nodes are configured
to send logs to the Admin node's logging service.  The service is also configured post-install as well.
The logging service stores per-node log files.

