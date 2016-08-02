.. index::
  pair: Objects; Providers

.. _arch_provider:

Provider Usage
==============

.. index::
  TODO; provider_split_out
  pair: Provider; Provider usage

TODO: Use this part in arch
TODO: Put some in user guide.
TODO: Reference from Deployment.

Overview
--------

Providers are intended to be used by the Rebar core to handle various aspects of node management.  Currently, they let Rebar create and manage nodes on external providers (such as AWS, Rackspace, and Packet).  In the future, their scope will be expanded to handle all aspects of node provisioning and network management.

Saving Config in dr_info
------------------------

For regular uses, provider credentials can be stored in the :ref:`dr_info`.

Supported Providers
-------------------

.. index::
  pair: Provider; Phantom
  pair: Supported Providers; Phantom

Phantom
~~~~~~~

The Phantom provider is the default provider type for internal Rebar
nodes.  Normally, nodes will not be seen or be operating with the
Phantom provider.

.. index::
  pair: Provider; Metal
  pair: Supported Providers; Metal

Metal
~~~~~

Rebar uses the Metal provider to manage bare-metal nodes that
it has direct control over.  In future releases of Rebar, the current
built-in provisioner and network management code will be folded into
the Metal provider.  Metal is the default Provider for all nodes
created via the :ref:`digital_rebar_api`.

.. index::
  pair: Provider; Amazon EC2
  pair: Supported Providers; Amazon EC2

Amazon EC2
~~~~~~~~~~

The Amazon EC2 provider is used to let Rebar create, reboot, and
delete Amazon EC2 virtual machines. In order to use it the following must be done:

* Create a new IAM user on Amazon.
* Make sure that IAM user has the rights to create, reboot, and delete EC2
  instances, along with ability to create and delete keys for those
  instances.
* Create a new Provider with the following Rebar CLI call::

    victor@m4700:~/src/digitalrebar/deploy/compose (master)
    $ rebar -U rebar -P rebar1 providers create \
       '{"name": "amazon-vl-test",
         "type": "AwsProvider",
         "auth_details": {
             "aws_access_key_id": "IAM_aws_access_key",
             "aws_secret_access_key": "IAM_secret_key_for_access_key",
             "region": "the-preferred-region"
         }
        }'

Once a new provider has been created, create EC2 instances
using that provider::

    victor@m4700:~/src/digitalrebar/deploy/compose (master)
    $ rebar -U rebar -P rebar1 nodes create \
        '{"name": "amazon-test-2.neode.net",
          "provider": "amazon-vl-test",
          "hints": {
              "use-proxy": false,
              "provider-create-hint": {
                  "flavor_id": "t2.small",
                  "image_id": "ami-b4a2b5d5"
              }
          }
         }'

This will create a t2.small node running Ubuntu 14.04 in the region
the provider was configured to use.  If the
'provider-create-hint' section of the JSON is omitted, the provider
will default to using a t2.micro instance running Ubuntu 14.04.

.. index::
  pair: Provider; Google Compute Engine
  pair: Supported Providers; Google Compute Engine

Google Compute Engine
~~~~~~~~~~~~~~~~~~~~~

The Google Compute Engine provider lets Rebar create, reboot, and
delete GCE virtual machines. In order to use it, the following must be done:

* Create a new project to use.
* Make sure the
 project has the Google Compute Engine API enabled.
* Create a new service account key with permission to create, delete,
  and reboot GCE instances in the project.  Be sure and save the
  generated JSON file somewhere secure where it can be accessed with
  the rebar CLI.
* Create a new Provider with the following Rebar CLI call::

    victor@m4700:~/src/digitalrebar/deploy/compose (master)
    $ rebar -U rebar -P rebar1 providers create \
    "{\"name\": \"gce-vl-test\",
      \"type\": \"GoogleProvider\",
      \"auth_details\": {
          \"google_project\": \"the-project-name\",
          \"google_json_key\": $(cat "/path/to/downloaded/token.json")
      }
     }"

Once the Provider is created, a GCE instances can be built using it::

    victor@m4700:~/src/digitalrebar/deploy/compose (master)
    $ rebar -U rebar -P rebar1 nodes create \
    '{"name": "gce-test-2.neode.net",
      "provider": "gce-vl-test",
      "hints": {
          "use-proxy": false,
          "provider-create-hint": {
              "machine_type": "n1-standard-2",
              "zone_name": "us-east1-b",
              "disks": [
                  {"autoDelete": "true",
                   "boot": "true",
                   "type": "PERSISTENT",
                   "initializeParams": {
                       "sourceImage": "projects/centos-cloud/global/images/centos-7-v20151104"
                   }
                  }
              ]
          }
      }
     }'

If the information in 'provider-create-hint', is omitted it will default
to then 'n1-standard-1' machine type, the 'us-central1-f' zone, and a
single disk with Ubuntu 14.04 as the installed OS.

.. index::
  pair: Provider; Packet
  pair: Supported Providers; Packet

Packet.net
~~~~~~~~~~

The Packet.net provider lets Rebar manage bare metal nodes provided by
Packet.  In order to use it, the following must be done:

* Create an account and an API key with Packet.
* Create a new Project at Packet, and record its ID.
* Create a new Provider using the following Rebar CLI call::

    victor@m4700:~/src/digitalrebar/deploy/compose (master)
    $ rebar -U rebar -P rebar1 providers create \
    '{"auth_details": {
          "project_token": "the-API-key",
          "project_id": "the-project-UUID"
      },
      "name": "RackN Packet Account",
      "type": "PacketProvider"
    }'

Once the Provider is created, it can be used to allocate bare
metal nodes from Packet::

    victor@m4700:~/src/digitalrebar/deploy/compose (master)
    $ rebar -U rebar -P rebar1 nodes create \
    '{"name": "packet-1.neode.net",
      "provider": "RackN Packet Account",
      "hints": {
          "use-proxy": false,
          "provider-create-hint": {
            "facility": "ewr1",
            "plan": "baremetal_1",
            "os": "centos_7",
            "hostname": "packet-1.neode.net"
          }
      }
    }'

.. index::
  pair: Provider; Testing
  pair: Supported Providers; Testing

Testing Provider
~~~~~~~~~~~~~~~~

The testing provider adds debugging instructions to the Amazon EC2 provider, so activity can be simulated without actually creating remote notes.

* Create a new Provider with the following Rebar CLI call::

    victor@m4700:~/src/digitalrebar/deploy/compose (master)
    $ rebar -U rebar -P rebar1 providers create \
       '{"name": "test-vl-test",
         "type": "AwsProvider",
         "auth_details": {
             "aws_access_key_id": "IAM_aws_access_key",
             "aws_secret_access_key": "IAM_secret_key_for_access_key",
             "region": "the-preferred-region",
             "debug": {
                "host_ip":"[address of a ssh/pingable node]",
                "boot_delay_time":0,
                "ssh_delay_time":0
             }
          }
        }'
