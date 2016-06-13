.. _workloads_installation:

General Installation
--------------------

Workloads are require a specific set of roles to be included in the Digital Rebar server before they can run.  Make sure that your server has been started with those roles in place.  We are actively making it easier to add roles, so workload scripts will soon be able to upload the needed roles as part of their installation.

All workload scripts leverage the Digital Rebar annealer to coordinate work.  That means that all of the requested tasks are loaded into the system as quickly as possible: generally as soon as the node placeholders appear but before they are fully provisioned.  Once the work has been queued, the scripts have completed their function.  By default, the scripts will appear to continue acting as they monitor the annealer.  During this time, users could stop the script and login to Rebar to monitor progress themselves.

Install workloads you need the Digital Rebar Deploy infrastructure:

  ::

  	mkdir ~/digitalrebar
  	cd ~/digitalrebar
  	git clone https://github.com/rackn/digitalrebar-deploy deploy

If you have added AWS provider credentials to :ref:`dr_info` then you could then deploy a Kubernetes workload as follows (see :ref:`kubernetes_workload` for mre details):

   :: 

  	cd ~/digitalrebar/deploy
  	workloads/kubernetes.sh --deploy-admin=aws --provider=aws --deployment-name=rebarrocks

Read more about :ref:`workload_parameters` or you can use ``--help`` to get a full list of options.


Developer Notes
~~~~~~~~~~~~~~~

The remote install and workload scripts do NOT play well with doing local development using :ref:`docker_admin`.  You should create a second deployment clone if you are using ``tools/docker-admin`` which takes over the ``../deployment`` directory.