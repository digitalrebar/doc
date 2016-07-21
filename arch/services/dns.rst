.. index::
  pair: Services; DNS
  pair: Services; DNS Management
  pair: Containers; DNS

.. _arch_service_dns:


DNS
===

The DNS Subsystem consists of three components: the server, management
server, and filters.

DNS Server and Service
----------------------

The Digital Rebar system can provide the DNS Server. Currently, the Digital Rebar DNS server is BIND. The BIND
server will set up everything needed run a DNS server. Any external DNS server could be used in place of this, but the server must be injected into the system by the common.env in
the deployment scripts.

DNS Management Server and Service
---------------------------------

The management server is used to rebuild files and inject information into the DNS server
and runs on the same system as the BIND DNS server. The management server can also manage a PowerDNS server
through its HTTP API (version 3.4.5 or higher). In this case, the management server
can be on any system. Currently, only external PowerDNS
servers can be managed remotely. The management server needs
additional information such as access tokens and
is provided as consul key/value pairs associated with the external
PowerDNS service injected into consul. These are also specified in
common.env file.

DNS Name Filters
----------------

The Name filters
provide a mechanism to generate names for address allocations on nodes.
These name/IP pairs are sent to a specified DNS management service that updates
the DNS server. Filters are ordered and evaluated. Once
matched, a name is generated and the service is called. A template system
is used to generate names from node attributes. All matching filters
will be applied.  See :ref:`api_dns_name_filter` and
:ref:`object_dns_name_filter` for more information.
