
.. note:: WARNING WARNING WARNING:  This is the Digital Rebar v2 product documentation.  That product line is EOL as of September 2017.  Please refer to the new Digital Rebar Provision v3 documentation:  http:\/\/provision.readthedocs.io\/en\/tip\/README.html

.. index::
  pair: Services; Web Proxy
  pair: Container; Web Proxy

.. _arch_service_webproxy:

Web Proxy
---------

The Web Proxy container runs a squid proxy that allows nodes to access sites outside of their cluster.  This
system is configured by default.  However, the squid proxy can be configured to use an upstream proxy server.  This is
particularly useful when dealing with corporate firewalls.  The system currently can't be turned off.
