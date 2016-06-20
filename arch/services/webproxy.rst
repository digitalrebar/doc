.. index::
  pair: Services; Web Proxy
  pair: Container; Web Proxy

.. _arch_service_webproxy:

Web Proxy
---------

The Web Proxy container runs a squid proxy that allows nodes to access sites external to the cluster.  This 
system is configured by default.  The squid proxy can be configured to use an upstream proxy server.  This is
particularly useful when dealing with corporate firewalls.  The system can not be currently turned off.

