.. index::
  pair: Services; Certificate
  pair: Container; Trust Me

.. _arch_service_trust_me:

Trust Me
--------

The Trust Me container provides certificate signing services for the Digital Rebar system.  As containers start
up, if they need access to other API services or provide external access, the container requests signed
certificate with a public/private key pair.  These are then used as server or client SSL endpoint certifcates
to control service access.  All components of the system allow access only if a client certificate is provided.
The one exception is the :ref:`arch_service_revproxy`.

The Trust Me container is based upon the cfssl tools and currently uses a single self-signed root chain.

