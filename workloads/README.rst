.. _workloads_guide:

Platform Workloads
==================

This guide will describe how to install and use Digital Rebar Workloads.

Workloads are groups of roles that deliver specific functionality such as platform as a service, container management and storage services.  They maybe often used in combination so users should expect to install multiple workloads together.

.. toctree::
   :glob:
   :numbered:
   :maxdepth: 2

   kubernetes/README
   swarm/README
   mesos/README

General Installation
--------------------

Workloads are require a specific set of roles to be included in the Digital Rebar server before they can run.  Make sure that your server has been started with those roles in place.  We are actively making it easier to add roles, so workload scripts will soon be able to upload the needed roles as part of their installation.

Install workloads you need the Digital Rebar Deploy infrastructure:

  ::
  
  	mkdir ~/digitalrebar
  	cd ~/digitalrebar
  	git clone https://github.com/rackn/digitalrebar-deploy deploy

Note: You can use ``--help`` to get a full list of options.

The following options are common for all workload scripts:

  * ``--deploy-admin=[provider]`` tells the script to create a new DR admin server on the provider specified.
  * ``--admin-ip=[ip]`` allows the script to use an existing DR admin server.  Generally, this is used with the ``--deployment-name`` option
  * ``--deployment-name=[name]`` sets the deployment for the workload.  This is needed when you are testing multiple workloads on the same admin server.  It also determines the names of the nodes created.

RECOMMENDATION: You can provide useful defaults for these scripts in your :ref:`dr_info` file.  This is also helpful to store your provider credentials.

For example, to install the :ref:`kubernetes_workload`, use:

  ::

  	cd ~/digitalrebar/deploy
  	workloads/kubernetes.sh --deploy-admin=google --provider=aws --deployment-name=rebarrocks

Using A Running DR Admin
~~~~~~~~~~~~~~~~~~~~~~~~

While workloads scripts often include a Digital Rebar admin setup (see :ref:`install`), it saves time if you already have a working admin node.  You can tell the scripts to use the admin node using ``--admin-ip=[ip]``.

Cleaning Up
~~~~~~~~~~~

Workloads respect the ``--teardown=true`` instruction to remove a workload.  Make sure to include the same ``--deployment-name``!  This only works if you've used the ``--deploy-admin`` option.

If you want to keep the Admin node running for additional deployments, include the ``--keep-admin=true`` flag.  It defaults to _false_.

Providers
~~~~~~~~~

Workloads need to :ref:`ug_add_provider`, so expect that you will need to specify a provider.

Developer Note
--------------

The remote install and workload scripts do NOT play well with doing local development using :ref:`docker_admin`.  You should create a second deployment clone if you are using ``tools/docker-admin`` which takes over the ``../deployment`` directory.