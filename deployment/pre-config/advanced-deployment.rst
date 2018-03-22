
.. note:: WARNING WARNING WARNING:  This is the Digital Rebar v2 product documentation.  The v2 version is EOL as of September 2017.  Please refer to the new Digital Rebar Provision v3 documentation:  http:\/\/provision.readthedocs.io\/en\/tip\/README.html



.. index::
  pair: Deployment; Customization

.. _advance_deployment:

Advanced Deployments
~~~~~~~~~~~~~~~~~~~~

While Docker-based developments or simple developments can function
with the default configuration, in many cases some level of customization will be required.  From
networking to external services to initial configuration values, the
rebar-config.sh script currently controls how the admin components are
deployed.

The production.sh script is used to stage, install, and configure
the initial Digital Rebar admin server.  The customization of the rebar-config.sh
script allows for additional configurations and modifications.

`External Services <./external-services.md>`__ describes how to turn off
services in Digital Rebar and use external replacements.

Another customization allowed is around networking.  The default system
configuration assumes that the admin network will contain the admin
server.  This allocation is done by the following line:

::

    rebar roles bind "network-$admin_net_name" to "$FQDN"

Commenting this line out will stop the allocation of an admin address for that
network.  The admin server providing the :ref:`arch_service_provisioner` will need to be
routable from the other admin networks to the network that the admin server is
on.  The implication of this is that the :ref:`arch_other_systems` does not have to be
on an admin network.  It just has to be routable to admin networks.

The network category system allows for the creation of multiple admin
networks.  Creating a new network is accomplished by adding a new network
with a category of *admin*.  The :ref:`arch_service_dhcp` server, if configured, will update
and serve that network as well.  The only assumption is that the new
admin network has DHCP relay agent or helper that forwards the DHCP
requests to the admin node or has a DHCP server that forces the nodes to
PXE boot to the admin node.

The default Digital Rebar environment builds an admin network and a BMC
network that are paired by a common group field value.  Additional admin
networks can be joined to the existing BMC network by using the same
group.  If a different BMC network is needed, it can be created and
associated with its corresponding admin network through a commonv group
value.

If the admin node is not part of the admin network, additional networks
can be added at any time in the future.
