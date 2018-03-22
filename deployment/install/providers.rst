
.. note:: WARNING WARNING WARNING:  This is the Digital Rebar v2 product documentation.  That product line is EOL as of September 2017.  Please refer to the new Digital Rebar Provision v3 documentation:  http:\/\/provision.readthedocs.io\/en\/tip\/README.html

.. index::
  pair: Providers; Configuration

.. _configure_providers:

Configuring Providers
=======================

The following information applies to the cloud :ref:`ux_providers` in the UI.

**WARNING**: Provider configurations contain keys and tokens that allow users to request cloud resources.  This information should **not** be shared.  Do not screencast or share provider configuration unless the information is intended for the public.

Protip: See :ref:`ug_add_provider` to upload providers from a CLI.

Configuration
-------------

.. index::
  pair: Configuration; Google

Amazon Provider
~~~~~~~~~~~~~~~

The Amazon provider uses the API key and secret as the primary.  Users must also provide the region at the provider level.

Users may set a default subnet_id for the provider.  This subnet_id can be overriden at the node level.  Subnet_id must start with "subnet-" or it will be ignored.

**Note**: AMI IDs are region specific!

Google Provider
~~~~~~~~~~~~~~~

To get the Google Key, navigate to API Manager...Credentials...Create Credentials for Service Account.  Choose JSON key and download the service account key.  Then update the path to point to the used account file.  The upload system will automatically expand the file, so the actual JSON appears in the Provider credentials.

Make sure to use the project ID not the project name.  The project ID should include some extra digits that ensure uniqueness.

Packet Provider
~~~~~~~~~~~~~~~

The project ID for Packet is a full GUID.  This GUID can be found on the URL path when a project is selected in the Packet UI.

.. index::
  pair: Configuration; OpenStack

OpenStack Provider(s)
~~~~~~~~~~~~~~~~~~~~~

**Note**: If there is no private network one should be created.  Ideally, it is named "private" or "internal"

In the Horizon Dashboard, the provider details can be quickly obtained from Download RC file.

* SSH user (defaults to root, centos, ubuntu) is needed if system nodes do not use standard user accounts.  For example, AWS disables root and requires users to start with ``aws-user``.
* Debug Flag will include the credentials in the log when true.
* Networking is not consistent for OpenStack; however, the ``_auto_`` setting in :ref:`arch_service_cloudwrap` makes reasonable guesses about Network names including private and internal or public and external.  If the auto guess does not work, then simply provide the name of the network.  ``_none_`` can also be provided so that Cloudwrap does not attempt to resolve the matching network.

When troubleshooting OpenStack, use the debug=true flag.  This will provide the full OpenStack CLI command (including the credentials!) in the log.  This allows duplication of the Cloudwrap container actions using Docker exec: ``docker exec -it compose_cloudwrap_1 [openstack snip....]``.  This is a very handy way to test the OpenStack provider details.

DreamCompute:

* Auth-url: ``https://iad2.dream.io:5000/v2.0``
* ssh user: ``dhc-user``
* public network: ``auto``
* private network: ``auto``

Datacenterd.io:

* Auth-url: ``https://compute.datacentred.io:5000/``
* ssh user: ``centos ubuntu``
* public network: ``public``
* private network: ``private``

Vexxhost:

* Auth-url: ``https://auth.vexxhost.net/v2.0/``
* ssh user: ``centos ubuntu root``
* public network: ``public``
* private network: ``pprivate``

Auro.io:

* Auth-url: ``https://api.tor1.auro.io:5000/v2.0``
* ssh user: ``centos ubuntu``
* public network: ``ext-net``
* private network: ``Private``

Bluebox:

* Auth-url: per config
* ssh user: ``ubuntu centos``
* public network: ``internal``
* private network: per config


Rackspace:

* Auth-url: ``https://identity.api.rackspacecloud.com/v2.0/``
* ssh user: ``root ubuntu centos``
* public network: ``none``
* private network: ``none``

**Note**: Rackspace networking DOES create public and private networks but they do not show up in neutron.  Cloudwrap will handle the none-none case correctly here.

.. index::
  pair: Debugging; Provider

Debug Provider
~~~~~~~~~~~~~~

The Debug Provider creates Digital Rebar nodes without having a backing Infrastructure as a Service (IaaS).  It is helpful for testing scale and general workloads.  By default, there is a delay in provisioning debug nodes to help simulate actual node creation.

If a valid IP is provided to the Debug Provider then it will be able to advance the node workflow.

.. index::
  pair: Troubleshooting; Provider

.. _troubleshoot_providers:

Troubleshooting Tips
--------------------

It may take several attempts to get the Provider details exactly right.  This section helps resolve issues with the provider configuration.  Restarting the :ref:`arch_service_cloudwrap` container is not necessary when changing provider details, as they automatically synchronize.

It is recommended to manually create nodes during the testing phase.

The Cloud Providers use the Cloudwrap container to create and destroy remote nodes.  There are two phases for Cloudwrap operations: create/destroy actions via the API (api.rb) and then waiting (waiter.rb) for created nodes to be available for provisioning.

Digital Rebar creates a unique SSH key for each node.  When the node is available, a root account is created/updated with the Digital Rebar control key and the SSH key is removed.

Cloudwrap provides detailed logging in the container that helps to monitor the progress of Cloudwrap.  To monitor the logs access the Docker container that runs Cloudwrap.  The logs will allow the tracking of the creation of nodes and the waiting process.  By watching the IaaS system,matching provisioning actions and troubleshooting Cloudwap are possible.


  ::

    cd ~/digitalrebar/deploy/compose
    docker-compose logs cloud_wrap

REMINDER: Digital Rebar relies on ICMP (ping) and SSH (port 22) to validate that the node is running.  These ports must be open between the Digital Rebar admin and the node.
