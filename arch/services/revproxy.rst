
.. note:: WARNING WARNING WARNING:  This is the Digital Rebar v2 product documentation.  That product line is EOL as of September 2017.  Please refer to the new Digital Rebar Provision v3 documentation:  http:\/\/provision.readthedocs.io\/en\/tip\/README.html

.. index::
  pair: Services; Reverse Proxy
  pair: Container; Reverse Proxy

.. _arch_service_revproxy:

Reverse Proxy
-------------

The Reverse Proxy (revproxy) container runs custom golang program that handles user authentication and
request forwarding to the proper API or UX endpoint.  

The revproxy can provide a local file based user system or integrate with Okta to provide a single sign-on
experience.

