DNS Subsystem
=============

The DNS Subsystem consists of three components: the server, management
server, and filters.

DNS Server and Service
----------------------

The DNS server can be provided by the Digital Rebar system or
an external one can be used. Currently, the Digital Rebar DNS server is BIND. The BIND
server will set up everything needed run a DNS server. External DNS
server can be anything, but needs to be injected into the consul
services. This is done in rebar-config.sh. See that file for how to
select a server.

DNS Management Server and Service
---------------------------------

The management server is used to rebuild files and inject information into the DNS server and runs on the same system as the BIND DNS server. The management server can also manage a PowerDNS server
through its HTTP API (version 3.4.5 or higher). In that case, the management server
can be on any system. Currently, only external PowerDNS
servers can be managed remotely. The management server needs
additional information like access token and
are provided as consul key/value pairs associated with the external
PowerDNS service injected into consul. These are also specified in
rebar-config.sh along with external service registration.

DNS Name Filters
----------------

The third component of the DNS subsystem are filters. The Name filters
provide a mechanism to generate names for address allocations on nodes.
These name/IP pairs are sent to a specified DNS management service to
handle updating the DNS server. Filters are ordered and evaluated. Once
matched, a name is generated and the service is called. A template system
is used to generate names from node attributes. All matching filters
will be applied.
