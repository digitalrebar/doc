Deployments
===========

Deployments provide functional scope for Digital Rebar.  The **system** deployment has special meaning in Digital Rebar; consequently, to do non-discovery operations on a node, it must be part of a deployment.

.. image:: /images/screens/dr_nodes_provider_enabled.png


Create a deployment from the Deployment...Deployments (``/deployments``)
page. Provide the name for your deployment (default is ``default``) and
click the ``add`` button.

Once the deployment is created, you can navigate directly to the
deployment from the Deployment...Deployments submenu or direct using
``/deployments/[my deployment]``.

    Deployments are automatically set to have the system deployment as
    their parent. In the future, other parents may be set.

Adding Nodes to a Deployment
~~~~~~~~~~~~~~~~~~~~~~~~~~~~

Once you have a deployment, you must attach nodes to it before you can
take further action.

You can set a node into a deployment from the Nodes list drill down into
each node page (``/nodes/[node name]``) or several at a time from the
Nodes...Bulk Edit (``/dashboard/list``). Both methods provide a list of
available deployments.

Adding Networks to a Deployment
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

Generally, deployments also configure one or more networks.

To create a network, visit the Network...Networks page (``/networks``)
and fill out the table row for your network making sure to select your
deployment. Click ``add`` to create the network.

Creating a network will also create a matching ``network-[name]`` role
in the system. These roles allow you to bind the network definition to
specific nodes in later steps.

    Once you create a network, you cannot change the assigned network.

Adding Roles to a Deployment
~~~~~~~~~~~~~~~~~~~~~~~~~~~~

The new deployment page should now have a list of assigned nodes. Digital Rebar
uses roles to determine the specific configuration required for a
deployment. You manage the deployment using special purpose milestone
roles (aka "noop") that represent target states. Digital Rebar tracks the
subroles needed to achieve the milestone and automatically adds them.

To add a milestone role, select it from the list at the top of the
screen and click ``add role``. For these instructions, use the
``O/S Installed`` role to install an operating system.

Once a role is added to a deployment, Digital Rebar will add it an it's
dependencies as columns into the deployment matrix.

Clicking on the role header will allow you to make deployment wide
configuration changes if that role has configuration settings.

Installing an OS on a Node
~~~~~~~~~~~~~~~~~~~~~~~~~~

To install an operating system on a node, you must attach the
``O/S Installed`` milestone role to the node.

To attach the O/S role to the node, you much click the green plus
button. This will automatically add both the ``O/S Installled`` and
``Install O/S`` role.

Once the O/S role is attached, the icon changes to a wrench. Clicking
the wrench on the ``Install O/S`` role allows you to choose which
operating system Digital Rebar will deploy if you've added multiple boot ISOs.

Once the roles are attached, you start the process by clicking the
``commit`` button.

Once the deployment is committed, Digital Rebar will automatically reboot the
node and start the O/S install process.
