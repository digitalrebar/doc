.. _ux_deployment:

Deployments
===========


This page displays the deployments in progress.  From this page, the nodes involved in the deployments, the roles applied to the nodes, the progress of node deployment, and the presence of errors are all visible.

Deployments can be added via the ``Create Deployment`` button in the bottom right hand corner.


Deployments Bar
~~~~~~~~~~~~~~~

Deployments can be seen below the header as a color-coded bar with the deployment name.  A green bar represents an active deployment, blue is proposed, yellow is committed, and red has encountered an error.

.. image:: /images/screens/webux/Deployment.png

 

Nodes and Roles
---------------

Within each drop-down bar, all of the nodes running in the deployment are shown.  On the left, each node has a circular icon that displays the overall status of the node.  Node roles extend horizontally from the node, with each role represented by its own circular icon.  These icons all follow the same color scheme as the deployments bar, and provide access to individual nodes or roles when clicked.

.. image:: /images/screens/webux/deploy_matrix.png


Tracking Progress of a Deployment
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

:ref:`ux_nodes` may have different role assignments in the same deployment.  For example, cloud and metal nodes will have different roles.  Power or reservation state will be shown as a prefix to the node name.

.. image:: /images/screens/webux/track_nodes.png

When Digital Rebar is working, node role states will be automatically updated in the deployment.


Adding Nodes to a Deployment
----------------------------

Once a deployment has been created, nodes must be attached before any further actions can be taken. At the bottom of each deployment, there are three buttons: Propose, Add Node, and Bind Node Roles.

.. image:: /images/screens/webux/no_propose.png

Select the ``Add Node`` icon at the bottom of the deployment to create a new node. 

To add existing nodes to a deployment, first navigate to the Nodes page. From this page, select the desired nodes then click the ``Move Nodes`` button in the upper right corner.

.. image:: /images/screens/webux/move_nodes.png


Adding Roles to a Deployment
----------------------------

To add a role, first click the ``Propose`` button at the bottom of the deployment. This will cause two new icons to appear: "add role" and "commit".

.. image:: /images/screens/webux/propose_use.png

Click the ``Add Role`` button and choose the desired role.

Once a role is added to a deployment, Digital Rebar will add it an it's
dependencies as columns into the deployment matrix.

Clicking on the role header will allow deployment wide
configuration changes if that role has configuration settings.

Adding Roles to a Node
----------------------

After adding a role to a deployment, it can be bound to a node by clicking the ``Bind Node Roles`` button. After choosing the desired role, click the plus button beside the node you wish to modify.

Once the roles are attached, the process can be started by clicking the
``Commit`` button.

Once the deployment is committed, Digital Rebar will automatically reboot the
node and start the install process.


Adding Networks to a Deployment
-------------------------------

Generally, deployments also configure one or more networks.

To create a network, visit the Networks page and fill out the table for the network making sure to select the
deployment.  Click ``add`` to create the network.

Creating a network will also create a matching ``network-[name]`` role
in the system.  These roles allow the network definition to be bound to
specific nodes in later steps.

Once a network is created, the assigned network cannot be changed.





