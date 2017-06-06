.. _ux_deployment:

Deployments
===========


This page displays the deployments in progress. From this page, the nodes involved in the deployments, the roles applied to the nodes, the progress of node deployment, and the presence of errors are all visible.  


Deployments Bar
~~~~~~~~~~~~~~~

Deployments can be seen below the header as a bar with the deployment name. There is a circular progress meters, and a symbol that indicates the status of the node. Additionally, the bars are color-coded. Green shows active, while blue, yellow, and gray show proposed, committed, and error respectively.

.. image:: /images/screens/webux/deployment.png

Take note of the "Nodes" and "Roles" tabs. 
 

Nodes
-----

The "Nodes" tab is the default tab and shows all of the nodes running in the deployment. Nodes will appear color-coded like the bar and can be individually accessed by simply clicking on the node icon. 

.. image:: /images/screens/webux/deploy_nodes.png

Roles
-----

The "Roles" tab shows every node role being run by the nodes and allows them to be accessed. The tab is most useful for viewing node role deployment progress.  

.. image:: /images/screens/webux/deploy_roles.png

Matrix
------

The "Matrix" tab shows a composite of both the "Node" and "Roles" tabs. From there, all the nodes and node roles can be seen and accessed. 


.. image:: /images/screens/webux/deploy_matrix.png


Propose
-------

Beneath the node icons, there are three buttons: Propose, Add Node, and Bind Node Roles.
These can be used to add new roles, add new nodes, and bind roles to nodes respectively.

.. image:: /images/screens/webux/no_propose.png

**Note:** When Propose is opened two new icons will appear: "add role" and "commit. These are used to add a role and save the new role to the deployment respectively.

.. image:: /images/screens/webux/propose_use.png
