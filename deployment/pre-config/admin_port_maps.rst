.. index::
  pair: Admin Node; Port Mapping

.. _port_mapping:

Rebar Admin Node Port Mapping
-----------------------------

The following table can help determine which Digital Rebar services are
running on the admin server.  Depending on the configuration, they may not have to be exposed.

Please review and edit these port numbers.

.. index::
  pair: General Ports; Admin Node
  Ports; General Ports

General Ports for Admin
~~~~~~~~~~~~~~~~~~~~~~~

-  *443* - Chef API (externally mapped by Docker)
-  4646 - Chef Server
-  8300 - Consul
-  8301 - Consul
-  8302 - Consul
-  8400 - Consul
-  8500 - Consul UI (externally mapped by Docker)
-  8600 - Consul
-  8888 (certificate signing service and ICMP)

.. index::
  pair: General Ports; Managed Nodes

General Ports for Managed Nodes
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

-  22 - SSH

.. index::
  Ports; Specific Ports
  Specific Ports; Kubernetes
  Kubernetes; Ports

Kubernetes Specific
~~~~~~~~~~~~~~~~~~~


.. index::
  pair: Ports; Physical Infrastructure

Physical Infrastructure Ports
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

-  53 - DNS
-  68 - DHCP
-  123 - NTP
-  514 - SYSLOG
-  953 - RNDC
-  6754 - DNS Mgmt Server
-  8091 - TFTP Server (provides PXE images)
-  8123 - Squid Proxy
-  9991 - DHCP Management Port

.. index::
  pair: Ports; Internal

Internal Ports
~~~~~~~~~~~~~~

-  5432 - Postgresql Database
