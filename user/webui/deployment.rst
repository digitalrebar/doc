.. index::
  pair: Deployment; Web UI

.. _webui_deployment:

Deployments
===========

Deployments provide functional scope for Digital Rebar.  The **system** deployment has special meaning in Digital Rebar. Consequently, to do non-discovery operations on a node, it must be part of a deployment.

.. image:: /images/screens/dr_nodes_provider_enabled.png


Create a deployment from the Deployment...Deployments (``/deployments``)
page. Provide the name for the deployment (default is ``default``) and
click the ``add`` button.

Once the deployment is created, there is the option to navigate directly to the
deployment from the Deployment...Deployments submenu or direct using
``/deployments/[my deployment]``.

    Deployments are automatically set to have the system deployment as
    their parent. In the future, other parents may be set.

Deployment without Nodes
------------------------

A deployment can exist without :ref:`ui_nodes`.  In this mode, it is possible to add :ref:`ui_roles` and change the deployment state from proposed to committed and back.

.. image:: /images/screens/dr_system_no_nodes.png

Once nodes have been added, the deployment will show the node-role state for the nodes.

.. image:: /images/screens/dr_single_deployment.png

Use the (+) button to add roles to nodes as desired.

Tracking Progress of a Deployment
---------------------------------

:ref:`ui_nodes` may have different role assignments in the same deployment.  For example, cloud and metal nodes will have different roles.  Power or reservation state will be shown as a prefix to the node name.

.. image:: /images/screens/dr_system_cloud_and_metal.png

When Digital Rebar is working, node-role states will be automatically updated in the deployment.

.. image:: /images/screens/dr_system_new_nodes.png

Adding Nodes to a Deployment
~~~~~~~~~~~~~~~~~~~~~~~~~~~~

Once a deployment has been created, nodes must be attached before any further actions can be taken.

A node can be set into a deployment from the Nodes list drill down into
each node page (``/nodes/[node name]``) or several at a time from the
Nodes...Bulk Edit (``/dashboard/list``). Both methods provide a list of
available deployments.

.. image:: /images/screens/dr_bulk_edit.png


Adding Networks to a Deployment
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

Generally, deployments also configure one or more networks.

To create a network, visit the Network...Networks page (``/networks``)
and fill out the table row for the network making sure to select the
deployment. Click ``add`` to create the network.

Creating a network will also create a matching ``network-[name]`` role
in the system. These roles allow the network definition to be bound to
specific nodes in later steps.

    Once a network is created, the assigned network cannot be changed.

Adding Roles to a Deployment
~~~~~~~~~~~~~~~~~~~~~~~~~~~~

The new deployment page should now have a list of assigned nodes. Digital Rebar
uses roles to determine the specific configuration required for a
deployment. The deployment can be managed using special purpose milestone
roles (aka "noop") that represent target states. Digital Rebar tracks the
subroles needed to achieve the milestone and automatically adds them.

To add a milestone role, select it from the list at the top of the
screen and click ``add role``. For these instructions, use the
``O/S Installed`` role to install an operating system.

Once a role is added to a deployment, Digital Rebar will add it an it's
dependencies as columns into the deployment matrix.

Clicking on the role header will allow deployment wide
configuration changes if that role has configuration settings.

Installing an OS on a Node
~~~~~~~~~~~~~~~~~~~~~~~~~~

To install an operating system on a node, attach the
``O/S Installed`` milestone role to the node.

To attach the O/S role to the node, click the green plus
button. This will automatically add both the ``O/S Installled`` and
``Install O/S`` role.

Once the O/S role is attached, the icon changes to a wrench. Clicking
the wrench on the ``Install O/S`` role allows choice over which
operating system Digital Rebar will deploy if multiple boot ISOs were added.

Once the roles are attached, the process can be started by clicking the
``commit`` button.

Once the deployment is committed, Digital Rebar will automatically reboot the
node and start the O/S install process.
