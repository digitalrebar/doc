.. index::
	pair: Installation; Workloads

.. _workloads_installation:

General Installation
--------------------

Workloads require a specific set of roles to be included in the Digital Rebar server before they can run.  Make sure that the server has been started with these roles in place.  We are actively making it easier to add roles, so workload scripts will soon be able to upload the needed roles as part of their installation.

All workload scripts leverage the Digital Rebar annealer (see :ref:`simulated_annealing`) to coordinate work.  That means that all of the requested tasks are loaded into the system as quickly as possible: generally as soon as the node placeholders appear but before they are fully provisioned.  Once the work has been queued, the scripts have completed their function.  By default, the scripts will appear to continue acting as they monitor the annealer.  During this time, users could stop the script and login to Rebar to monitor progress themselves.

To install the required workloads, the Digital Rebar Deploy infrastructure is needed:

  ::

  	mkdir ~/digitalrebar
  	cd ~/digitalrebar
  	git clone https://github.com/rackn/digitalrebar-deploy deploy

Make sure to open the correct port, see :ref:`port_mapping`.

If AWS provider credentials have been added to :ref:`dr_info`, then a Kubernetes workload can be deployed as follows (see :ref:`kubernetes_workload` for more details):

   :: 

  	cd ~/digitalrebar/deploy
  	workloads/kubernetes.sh --deploy-admin=aws --provider=aws --deployment-name=rebarrocks

Read more about :ref:`workload_parameters` or use ``--help`` to get a full list of parameters.

Developer Notes
~~~~~~~~~~~~~~~

The remote install and workload scripts do NOT play well with doing local development using :ref:`docker_admin`.  Create a second deployment clone if ``tools/docker-admin`` is being useed because it takes over the ``../deployment`` directory.