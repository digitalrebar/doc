.. _providers:

Providers
=========

Providers allow Digital Rebar to interact with Infrastructure as a Service (IaaS or Cloud) providers.  These providers are able to "create" and "destroy" servers programatically.  If a node is created with a non-metal provider, then Digital Rebar will use the information in the Provider to acquire servers.

.. image:: /images/screens/dr_providers_list.png

For details, see :ref:`configure_providers` about configuration and :ref:`troubleshoot_providers`

Nodes via Providers
-------------------

When a node has been created with a provider, it will appear in the nodes with in the regular way.  Provider created nodes are not available to Digital Rebar until the Provider has uploaded the Digital Rebar ssh keys.

.. image:: /images/screens/dr_cloud_provider_working.png

WARNING: It is possible for node create and destroy to fail in such a way that the resources have been created on the IaaS provider but do not appear in Digital Rebar!  This can create unexpected costs with providers.

Adding Providers
----------------

Providers can be added by selecting a provider type in the top right of the Provider list.

.. image:: /images/screens/dr_providers_initial.png

And then exiting the appropriate fields.

.. image:: /images/screens/dr_provider_aws.png

Developer Notes
---------------

Provider activity can be monitored by watching the Cloudwrap container logs.  See ref:`configure_providers` for details.