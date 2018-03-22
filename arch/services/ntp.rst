
.. note:: WARNING WARNING WARNING:  This is the Digital Rebar v2 product documentation.  That product line is EOL as of September 2017.  Please refer to the new Digital Rebar Provision v3 documentation:  http:\/\/provision.readthedocs.io\/en\/tip\/README.html

.. index::
  pair: Services; NTP
  pair: Container; NTP

.. _arch_service_ntp:

NTP
---

The NTP container provides the configuration of the NTP subsystem as specified in common.env.

The container can be run with or without an NTP daemon.  If it is configured as a PROXY, the container will
run NTP and synchronize to a set of upstream servers (if specified).  If PROXY is not specified, but the 
EXTERNAL_SERVERS are specified, the nodes will be configured to talk to those servers.
