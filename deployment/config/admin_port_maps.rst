.. _port_mapping:

Rebar Admin Node Port Mapping
-----------------------------

The following table can help figure out which Digital Rebar services are
running on the admin server:

General Ports:

-  22 - SSH
-  *443* - Chef API (externally mapped by docker)
-  *3000* - Rebar API & UI (externally mapped by Docker)
-  4646 - Chef Server
-  8300 - Consul
-  8301 - Consul
-  8302 - Consul
-  8400 - Consul
-  8500 - Consul UI (externally mapped by docker)
-  8600 - Consul

Additional Ports for Physical Infrastructure

-  53 - DNS
-  68 - DHCP
-  123 - NTP
-  514 - SYSLOG
-  953 - RNDC
-  5432 - Postgresql Database
-  6754 - DNS Mgmt Server
-  8091 - TFTP Server (provides PXE images)
-  8123 - Squid Proxy
-  9991 - DHCP Management Port

Please review and edit these port numbers.
