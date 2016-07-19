Connecting to the BMC Network
-----------------------------

| By default, Rebar sets up a BMC network on 192.168.128.xxx/24 named
  ``the_bmc`` in the category ``bmc`` and the group ``internal``.
| Changing values from the ``/networks`` page will modify the BMC network. These instructions have been created with the
  assumption of the default network and should be modified
  to match the specific configuration.

Attaching Admin to BMC
~~~~~~~~~~~~~~~~~~~~~~

While Rebar will configure the admin node and managed node BMCs, it does
not configure a gateway for the local workstation to connect to the nodes on
that network. A gateway IP ust be added on the BMC network from the local
system to connect to the BMC network.

These instructions assume a Linux desktop with the Admin
node running in a Docker container. The container is using docker0 as
the network bridge to the nodes.

BMC range must be added to the bridge from the local workstation:
``sudo ip addr add 192.168.128.1/24 dev docker0``

The node's BMC interfaces should now be pingable. By default
they are assigned on from 192.168.128.21, so ``ping 192.168.128.21``
should work.

The IPs for the BMC network should be visible on the ``/network_map``
page in the UI and node detail page.

Remote Manage Web UI
~~~~~~~~~~~~~~~~~~~~

Once aware of the node's BMC IP address and have network access to that
network, he node's Web Management interface should be accessable
(if the node has one).

From a browser: ``https://[node ip]`` should bring up a login prompt.

The default login is ``root``/``cr0wBar!``