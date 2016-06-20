.. index::
  pair: Services; Reverse Proxy
  pair: Container; Reverse Proxy

.. _arch_service_revproxy:

Reverse Proxy
-------------

The Reverse Proxy (revproxy) container runs custom golang program that handles user authentication and
request forwarding to the proper API or UI endpoint.  

The revproxy can provide a local file based user system or integrate with Okta to provide a single sign-on
experience.

