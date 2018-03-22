
.. note:: WARNING WARNING WARNING:  This is the Digital Rebar v2 product documentation.  The v2 version is EOL as of September 2017.  Please refer to the new Digital Rebar Provision v3 documentation:  http:\/\/provision.readthedocs.io\/en\/tip\/README.html

.. _ux_providers:

Providers
=========

The "Provider" page simply displays the available providers, the provider's types, the descriptions, and the tenant of the provider. Providers allow Digital Rebar to interact with Infrastructure as a Service (IaaS) or Cloud providers.  These providers are able to "create" and "destroy" servers programmatically.  If a node is created with a non-metal provider, then Digital Rebar will use the information in the Provider to acquire servers.

.. image:: /images/screens/webux/Provider.png

For details, see :ref:`configure_providers` about configuration and :ref:`troubleshoot_providers`.

Adding Providers
----------------

Providers can be added by selecting ``Add Provider`` in the bottom right of the Provider page.

.. image:: /images/screens/webux/add_provider.png

Developer Notes
---------------

Provider activity can be monitored by watching the Cloudwrap container logs.  See :ref:`configure_providers` for details.
