.. index::
  pair: Workloads; Parameters

.. _workload_parameters:

Workload Parameters 
-------------------

**Note**: *These parameters are optional!*

The following options are common for all workload scripts:

  * ``--deploy-admin=[provider]`` tells the script to create a new DR admin server on the provider specified.
  * ``--admin-ip=[ip]`` allows the script to use an existing DR admin server.  Generally, this is used with the ``--deployment-name`` option
  * ``--deployment-name=[name]`` sets the deployment for the workload.  This is needed when testing multiple workloads on the same admin server.  It also determines the names of the nodes created.
  * ``--wait-on-converge=true|false`` tells the script to wait for converge work created by the script.  This assumes that the admin is only doing one script at a time and is not recommended for CI/CD testing or parallel testing.  Defaults to ``true``
  * ``--rebar-password=<String>`` sets the password to access the rebar system.  Defaults to ``rebar1``.
  * ``--rebar-user=<String>`` changes the Username to access the rebar system.  Defaults to ``rebar``.

RECOMMENDATIONS: 

  * Defaults can be provided for these settings scripts in the :ref:`dr_info` file that is also used to store provider credentials.
  * Since the scripts will automatically install the :ref:`rebar_cli`, CLI commands can be used to access and test the cluster using the Admin End Point URL.

For example, to install the :ref:`kubernetes_workload`, use:

  ::

  	cd ~/digitalrebar/deploy
  	workloads/kubernetes.sh --deploy-admin=google --provider=aws --deployment-name=rebarrocks

The script can be interrupted while it is waiting to converge without impacting the deployment operation.

Using A Running DR Admin
~~~~~~~~~~~~~~~~~~~~~~~~

While workloads scripts often include a Digital Rebar admin setup (see :ref:`workloads_installation`), it saves time if a working :ref:`arch_other_systems` is already present.  Tell the scripts to use the admin node using ``--admin-ip=[ip]``.

Cleaning Up
~~~~~~~~~~~

Workloads respect the ``--teardown`` instruction to remove a workload.  Make sure to include the same ``--deployment-name``!  This only works if the ``--deploy-admin`` option was used.

In order to keep the Admin node running for additional deployments, include the ``--keep-admin=true`` flag.  Otherwise, it will default to _false_.

.. index::
  pair: Workloads; Providers

Providers
~~~~~~~~~

Workloads need to :ref:`ug_add_provider`, so expect to specify a provider.

  * ``--device-id=<String>`` allows users to continue an aborted script against a node that was created by a provider in a previous run.  This is very handy when debugging scripts.
  * ``--init-id-file=<file>`` File that defines the initial identity used to log into the node after provider provisioning.  The scripts will generally handle this automatically and this setting can be used if the provider limits the number of keys that can be used.

AWS Specific Options:

  * ``--provider-aws-admin-instance-type`` allows AWS instance types to be used for admin nodes.  This is important when running large tests and want extra resources.
  * ``--provider-aws-instance-type`` allows AWS instance types to be used for nodes to match performance needs.
  * ``--provider-aws-region`` chooses region to be used for nodes

Google Specific Options:

  * ``--provider-google-admin-instance-type`` allows Google instance types to be used for admin nodes.  This is important when running large tests and want extra resources.
  * ``--provider-google-instance-type`` allows Google instance types to be used for nodes to match performance needs.
  * ``--provider-google-zone`` chooses zone to be used for nodes

Advanced Options
~~~~~~~~~~~~~~~~

These options provide extra control for the Digital Rebar installation.

  * ``--dns-domain`` Domain name setting is important if nodes need to be joined to a larger DNS infrastructure.  Defaults to ``neode.local``
  * ``--dr_tag=<TAG>`` if running stable or special branches, then pick a build tag to use for digitalrebar.  default: ``latest``
  * ``--id-file=<file>`` picks the SSH Identity file to use to log into the node to ensure keys are in place.  This is useful if multiple SSH identities are in use.
