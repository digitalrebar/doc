.. _deploy_networks:

Network Deployment Guide
========================

Configuring networks in Digital Rebar requires knowledge of the desired networking environment.

**Note**: networks automatically create roles with matching names.  These roles much be attached to the nodes for the network to be configured on the node.

Need Details? Watch the Video! https://youtu.be/5YWMlYYuu-s

Network Settings
----------------

Digital Rebar networks names are system created based on the category and group.  This design allows automation of a single logical network across layer 2 boundaries.


Digital Rebar DHCP server is ONLY updated for networks categories named admin!  Because of groups, you can have multiple networks with an admin category!

The DHCP server cares about the subnet and conduit interface.  Digital Rebar will not act as a DHCP server unless the DHCP range matches the network(s) that Digital Rebar is using.  Also, you can bind the DHCP server to different/multiple interfaces using the conduit maps.  Use "dhcp" as the conduit for all interfaces.

Ranges (required)
-----------------

If you have a DHCP system then DO NOT TURN ON the lease functions!

  * dhcp named ranges generally allow anonymous leases
  * host named ranges generally have reserved leases


Router (optional) 
-----------------

Setting a router instructs the network to setup a router address when it builds the network.
