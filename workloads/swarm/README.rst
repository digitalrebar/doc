.. index::
	pair: Docker Swarm; Workloads

.. _swarm_workload:

Docker Swarm Workload
=====================

.. index::
  TODO; Describe_Docker_Swarm


Install the Docker Swarm workload from the ``digitalrebar/deploy`` directory using the ``workloads/docker-swarm.sh`` script.

Installation
------------

This section is specific to Docker-Swarm. See :ref:`workloads_guide` for general install tips.

   :: 

  	cd ~/digitalrebar/deploy
  	workloads/docker-swarm.sh --deploy-admin=aws --provider=aws --deployment-name=rebarrolls


Bidirectional Admin
~~~~~~~~~~~~~~~~~~~ 

The Docker Swarm install uses Chef script.  For this reason, the nodes must have access to the Admin.

Options
~~~~~~~

  * ``--docker-swarm-manager-count=<Number>`` Number of managers to start
  * ``--docker-swarm-member-count=<Number>`` Number of members to start
