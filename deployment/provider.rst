Provider Usage
==============

Overview
--------

Providers are intended to be used by the Rebar core to handle various aspects of node management.  For now, they just let Rebar create and manage nodes on external providers (such as AWS, Rackspace, and Packet).  In the future, though, their scope will be expanded to handle all aspects of node provisioning and network management.

Creating a new Provider
-----------------------

The simplest way to create a new Provider is via the rebar CLI:

.. code:: bash
   victor@m4700:~/src/digitalrebar/deploy/compose (master)
   $ rebar -U rebar -P rebar1 providers create \
       '{"name": "amazon-vl-test",
         "type": "FogProvider",
         "auth_details": {
             "provider": "AWS",
             "aws_access_key_id": "your_aws_access_key",
             "aws_secret_access_key": "secret_key_for_access_key",
             "region": "us-west-2"
         }
        }'

This tells Rebar to create a new Provider using the FogProvider
service.  The name field is required and must be globally unique among
providers, and the type field must contain the name of the external
service that this provider will use to control the nodes.  The
auth_details field is unique to each provider, and how it is
interpreted is up to the type of the provider.

Creating a node using a specific Provider
-----------------------------------------

To create a node using a specific Provider, pass the provider name as the node variant:

.. code:: bash
   victor@m4700:~/src/digitalrebar/deploy/compose (master)
   $ rebar -U rebar -P rebar1 nodes create \
       '{"name": "aws-test-1.neode.net",
         "variant": "amazon-vl-test",
         "hints": {
             "use-proxy": false,
             "provider-create-hint": nil
         }
       }'

This will create the node using the amazon-v1-test provider.  Note
that the node will not be ready for immediate use -- it will not have
any initial roles bound to it and it will be marked as not alive and
not available.  Once the node has bootstrapped and the FogProvider
service can contact it, the service will inject all the information
Rebar needs to control it and mark it alive and available.

Customizing the nodes to be created
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

TBA, but if you know Fog you should be able to guess the additional
parameters to pass in provider-create-hint.
