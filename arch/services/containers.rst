
.. note:: WARNING WARNING WARNING:  This is the Digital Rebar v2 product documentation.  That product line is EOL as of September 2017.  Please refer to the new Digital Rebar Provision v3 documentation:  http:\/\/provision.readthedocs.io\/en\/tip\/README.html

.. index::
  pair: Containers; Services

.. _arch_containers:

Collection of Container-based Services
--------------------------------------

Digital Rebar runs all of its the infrastructure management functions in Docker containers. Consequently, an environment that can run Docker (including Macs) must be used.

+---------------------------------+--------------------------------------------------------+
+ Container                       + Purpose                                                |
+=================================+========================================================+
| :ref:`arch_service_consul`      | Service Registry                                       |
+---------------------------------+--------------------------------------------------------+
| :ref:`arch_service_trust_me`    | Certficate Service for Identity Control                |
+---------------------------------+--------------------------------------------------------+
| :ref:`arch_service_postgres`    | Database for Object Storage                            |
+---------------------------------+--------------------------------------------------------+
| :ref:`arch_service_webproxy`    | Centralized Web Proxy to allow nodes internet access   |
+---------------------------------+--------------------------------------------------------+
| :ref:`arch_service_goiardi`     | Chef-like Server                                       |
+---------------------------------+--------------------------------------------------------+
| :ref:`arch_service_rebar_api`   | API and UX Server; Also containers job runners         |
+---------------------------------+--------------------------------------------------------+
| :ref:`arch_service_ntp`         | NTP Server                                             |
+---------------------------------+--------------------------------------------------------+
| :ref:`arch_service_cloudwrap`   | Provides Access to non-bare metal clouds               |
+---------------------------------+--------------------------------------------------------+
| :ref:`arch_service_dns`         | DNS Server and Management System                       |
+---------------------------------+--------------------------------------------------------+
| :ref:`arch_service_dhcp`        | DHCP Server and Management System                      |
+---------------------------------+--------------------------------------------------------+
| :ref:`arch_service_provisioner` | Provisioner Server and Management System               |
+---------------------------------+--------------------------------------------------------+
| :ref:`arch_service_logging`     | Logging Target for Nodes                               |
+---------------------------------+--------------------------------------------------------+
| :ref:`arch_service_ux`          | New Single Page Web-UX                                 |
+---------------------------------+--------------------------------------------------------+
| :ref:`arch_service_revproxy`    | Reverse Proxy that provides single endpoint for system |
+---------------------------------+--------------------------------------------------------+
| :ref:`arch_service_classifier`  | Rules-based Event Processor                            |
+---------------------------------+--------------------------------------------------------+
| :ref:`arch_service_forwarder`   | Alternate Front-end for Development Environments       |
+---------------------------------+--------------------------------------------------------+
