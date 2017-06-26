.. _ux_deployment:

Deployments
===========


This page displays the deployments in progress. From this page, the nodes involved in the deployments, the roles applied to the nodes, the progress of node deployment, and the presence of errors are all visible.  


Deployments Bar
~~~~~~~~~~~~~~~

Deployments can be seen below the header as a color-coded bar with the deployment name. A green bar represents an active deployment, blue is proposed, yellow is committed, and red has encountered an error.

.. image:: /images/screens/webux/Deployment.png

 

Nodes and Roles
---------------

Within each drop-down bar, all of the nodes running in the deployment are shown. On the left, each node has a circular icon that displays the overall status of the node. Node roles extend horizontally from the node, with each role represented by its own circular icon. These icons all follow the same color scheme as the deployments bar, and provide access to individual nodes or roles when clicked.

.. image:: /images/screens/webux/deploy_matrix.png

 

Propose
-------

Beneath the node icons, there are three buttons: Propose, Add Node, and Bind Node Roles.
These can be used to add new roles, add new nodes, and bind roles to nodes respectively.

.. image:: /images/screens/webux/no_propose.png

**Note**: When Propose is opened two new icons will appear: "add role" and "commit". These are used to add a role and save the new role to the deployment respectively.

.. image:: /images/screens/webux/propose_use.png
