.. _workloads_parameters:

Optional Parameters 
-------------------

The following options are common for all workload scripts:

  * ``--deploy-admin=[provider]`` tells the script to create a new DR admin server on the provider specified.
  * ``--admin-ip=[ip]`` allows the script to use an existing DR admin server.  Generally, this is used with the ``--deployment-name`` option
  * ``--deployment-name=[name]`` sets the deployment for the workload.  This is needed when you are testing multiple workloads on the same admin server.  It also determines the names of the nodes created.
  * ``--wait-on-converge=true|false`` tells the script to wait for converge work created by the script.  This assumes that the admin is only doing one script at a time and is not recommended for CI/CD testing or parallel testing.  Defaults to ``true``
  * ``--rebar-password=<String>`` sets the password to access the rebar system.  Defaults to ``rebar1``.
  * ``--rebar-user=<String>`` changes the Username to access the rebar system.  Defaults to ``rebar``.

RECOMMENDATIONS: 

  * You can provide defaults for these settings scripts in your :ref:`dr_info` file that is also used to store your provider credentials.
  * Since the scripts will automatically install the :ref:`rebar_cli`, you can use CLI commands to access and test your cluster using the Admin End Point URL.

For example, to install the :ref:`kubernetes_workload`, use:

  ::

  	cd ~/digitalrebar/deploy
  	workloads/kubernetes.sh --deploy-admin=google --provider=aws --deployment-name=rebarrocks

You can interrupt the script while it is waiting to converge without impacting the deployment operation.

Using A Running DR Admin
~~~~~~~~~~~~~~~~~~~~~~~~

While workloads scripts often include a Digital Rebar admin setup (see :ref:`install`), it saves time if you already have a working admin node.  You can tell the scripts to use the admin node using ``--admin-ip=[ip]``.

Cleaning Up
~~~~~~~~~~~

Workloads respect the ``--teardown`` instruction to remove a workload.  Make sure to include the same ``--deployment-name``!  This only works if you've used the ``--deploy-admin`` option.

If you want to keep the Admin node running for additional deployments, include the ``--keep-admin=true`` flag.  It defaults to _false_.

Providers
~~~~~~~~~

Workloads need to :ref:`ug_add_provider`, so expect that you will need to specify a provider.

  * ``--device-id=<String>`` allows users to continue an aborted script against a node that was created by a provider in a previous run.  This is very handy when debugging scripts.
  * ``--init-id-file=<file>`` File that defines the initial identity used to log into the node after provider provisioning.  The scripts will generally handle this automatically and this setting can be used if the provider limits the number of keys that can be used.

AWS Specific Options:

  * ``--provider-aws-admin-instance-type`` allows you to set AWS instance type to use for admin nodes.  This is important if you are running large tests and want extra resources.
  * ``--provider-aws-instance-type`` allows you to set AWS instance type to use for nodes to match your performance needs.
  * ``--provider-aws-region`` chooses region to use for nodes

Google Specific Options:

  * ``--provider-google-admin-instance-type`` allows you to set Google instance type to use for admin nodes.  This is important if you are running large tests and want extra resources.
  * ``--provider-google-instance-type`` allows you to set Google instance type to use for nodes to match your performance needs.
  * ``--provider-google-zone`` chooses zone to use for nodes

Advanced Options
~~~~~~~~~~~~~~~~

These options provide extra control for the Digital Rebar installation.

  * ``--dns-domain`` Domain name setting is important if you need your nodes to join a larger DNS infrastructure.  Defaults to ``neode.local``
  * ``--dr_tag=<TAG>`` if you are running stable or special branches, then pick a build tag to use for digitalrebar. default: ``latest``
  * ``--id-file=<file>`` picks the SSH Identity file to use to log into the node to ensure keys are in place.  This is useful if you have multple SSH identities.
