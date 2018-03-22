
.. note:: WARNING WARNING WARNING:  This is the Digital Rebar v2 product documentation.  That product line is EOL as of September 2017.  Please refer to the new Digital Rebar Provision v3 documentation:  http:\/\/provision.readthedocs.io\/en\/tip\/README.html

.. index::
  pair: Services; Certificate
  pair: Container; Trust Me

.. _arch_service_trust_me:

Trust Me
--------

The Trust Me container provides certificate signing services for the Digital Rebar system.  If containers need access to other API services or provide external access as they start up, the container requests a signed
certificate with a public/private key pair.  These certificates are then used as server or client SSL endpoint certificates
to control service access.  All components of the system allow access only if a client certificate is provided.
The one exception is the :ref:`arch_service_revproxy`.

The Trust Me container is based upon the CFSSL tools and currently uses a single self-signed root chain.
