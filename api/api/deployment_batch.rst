
.. note:: WARNING WARNING WARNING:  This is the Digital Rebar v2 product documentation.  That product line is EOL as of September 2017.  Please refer to the new Digital Rebar Provision v3 documentation:  http:\/\/provision.readthedocs.io\/en\/tip\/README.html

.. index::
  pair: Deployment; API

.. _api_deployment_batch:

Deployment Batch API
====================

For more detail on the Deployment API, see :ref:`api_deployment`

The Deployment Batch API is designed to allow users to quickly create deployments using a repeatable template.  Originally intended for use by the RackN Wizard, we were able to keep the format single and human readable so that it could be used as a portable deployment format.

Limitations: The batch assumes that the required roles have been installed, there is no facility at this time to import roles (via Barclamp import).  This may be addressed in future versions.

The batch call can be used against existing nodes and to create new nodes using a provider.  It is possible to mix these two modes.

The batch command will reviews all roles before applying any to the deployment and nodes.  This ensures correct ordering (based on cohort) of the roles.  The order of creation is as follows:

  1. nodes are created 
  #. deployment roles are added to the deployment
  #. attributes are set on the deployment roles
  #. node-roles are created assigned nodes into the deployment

Limitations: The batch is not smart enough (yet) to create nodes if a name is requested but does not exist.  [feature request]

Prerequisites
-------------

The batch requires the user to have created a deployment as a target for the batch operation.  That deployment must be in *proposed* mode for these changes to be accepted.  It is important to realize that the changes will not be automatically processed, the user is required to commit the deployment after batching before Digital Rebar will start processing.

API
---
PUT /api/v2/deployments/2/batch
POST /api/v2/deployments

If successful, the call will return the deployment targeted by the batch

UX
--

Users can batch templates using the RackN UX Wizard process


JSON Structure
--------------

Commit (optional)
~~~~~~~~~~~~~~~~~

A boolean value, the commit flag tells the system to commit the deployment after running the batch instruction.  This eliminates the user review stage and is helpful for automation using batch to streamline provisioning.


TLD (optional)
~~~~~~~~~~~~~~

A single value, the tld (top level domain) allows the user to specify a specific node name suffix.

Attribs (optional)
~~~~~~~~~~~~~~~~~~

A simple hash, the attribs hash contains a list of the attributes that should be set for this batch processing.  The values will be passed in as provided, so it is possible to provide multiple types or complex json inputs if needed.

**Note**: the batch process will not add new attributes; consequently, the attribs in Digital Rebar must exist before the batch is called.  

Side-effect: The batch will add the attribute's roles to the deployment.

Provider (optional)
~~~~~~~~~~~~~~~~~~~

A nested hash, the provider hash contains the name and hints used when the batch is creating new nodes.  Name is required and must exist in the system.  Hints are optional and depend on the provider type.

The top level provider is only used when no node level provider has been set.  This allows users to override the provider on a node by node basis.

Public_Keys (optional)
~~~~~~~~~~~~~~~~~~~~~~

A simple hash, the ``public_keys`` hash will add the passed keys into the Rebar Access list in the requested deployment so that users of the batch can get access to the nodes.

Use the form ``"public_keys":{"name1":"publickey1", "name2":"publickey2"}``

Nodes (required)
~~~~~~~~~~~~~~~~

An array of hashs, the nodes array contains the nodes and roles being applied in the batch.

**Note**: The nodes when created or moved are reassigned to use the tenant of the deployment.

Within each node hash, 

Required Fields in all cases:

  * roles: an array of roles to apply to this node

Fields in existing node cases

  * id: the id (numeric or name)  of the node to be used

Fields in create node cases

  * count (default 1 if missing) - the number of nodes like this to be created
  * provider (default to top level if missing) - the provider to use creating the nodes.  same synatax as the top level provider
  * description (default to username) - additional information

Optional Fields

  * prefix (defaults to ``node``): the name prefix of the node

the following keys are available
  * id (required for existing nodes, optional for new)

Role Apply Order (optional)
~~~~~~~~~~~~~~~~~~~~~~~~~~~

Under the key, "role_apply_order", users can provide an ordered array of roles passed into the processor to override the cohort ordering. 


JSON Example
------------

  ::

    {
      "tld":"batch.com",
      "commit": false,
      "public_keys": false,
      "provider": {
        "name": "debug-provider",
        "hints": {}
      },
      "attribs": {
        "k8s-cluster_name":"foo"
      },
      "nodes":[
        {
          "id": -1,
          "count": 2,
          "prefix": "cluster",
          "provider": {
            "name": "debug-provider",
            "hints": {}
          },
          "roles": 
          [
            "k8s-master"
          ]
        },
        {
          "count": 2,
          "prefix": "worker",
          "roles":
          [
            "k8s-worker"
          ]
        }
      ],
      "public_keys": {
        "name1": "key1"
      },
      "role_apply_order": [
        "etcd",
        "docker"
      ]
    }
