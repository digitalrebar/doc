Provider APIs
=============

Overview
--------

Providers encapsulate the methods needed to create, destroy, provision, and manage nodes.
This abstraction is still being defined, so the documentation is necessarily incomplete.

At a high level, a Provider is an interface to an external system such as Amazon AWS,
Rackspace, or Packet.net that is used to create and destroy Digital Rebar nodes on that system.
A provider must be able to handle the following tasks:

* Node creation
* Node removal
* Rebooting a node.
* Listing nodes that have been created.
* Getting information about the node.

In the future, providers will also handle more detailed node creation tasks, as well as configuring
and managing networks.

From the `Rebar API <../development/api>`_, you can perform the usual CRUD operations with providers

Rebar API Actions
~~~~~~~~~~~~~~~~~

+--------+-------------------------+----------------------------------------------------------+
| Verb   | URL                     | Comments                                                 |
+========+=========================+==========================================================+
| GET    | api/v2/providers        | List all the providers for all the providers             |
+--------+-------------------------+----------------------------------------------------------+
| GET    | api/v2/providers/:id    | Get information on a specific provider                   |
+--------+-------------------------+----------------------------------------------------------+
| GET    | api/v2/providers/create | Special case, returns no-db stub object for UI editing   |
+--------+-------------------------+----------------------------------------------------------+
| POST   | api/v2/providers        | Create a new provider for a provider.                    |
+--------+-------------------------+----------------------------------------------------------+
| DELETE | api/v2/providers/:id    | Delete an provider                                       |
+--------+-------------------------+----------------------------------------------------------+
| PUT    | api/v2/providers/:id    | Update an provider with new information.                 |
+--------+-------------------------+----------------------------------------------------------+
| PATCH  | api/v2/providers/:id    | Update an provider with new information using JSON Patch |
+--------+-------------------------+----------------------------------------------------------+


JSON Fields for Providers
~~~~~~~~~~~~~~~~~~~~~~~~~

+---------------+--------------+----------+----------------------------------------------------------+
| Attribute     | Type         | Settable | Note                                                     |
+===============+==============+==========+==========================================================+
| id            | Internal Ref | No       | Actually an Integer                                      |
+---------------+--------------+----------+----------------------------------------------------------+
| name          | String       | Yes      | Unique name for the provider.                            |
+---------------+--------------+----------+----------------------------------------------------------+
| description   | String       | Yes      | Description of the provider.                             |
+---------------+--------------+----------+----------------------------------------------------------+
| type          | String       | Yes      | The class of the provider for this provider.             |
+---------------+--------------+----------+----------------------------------------------------------+
| auth\_details | JSON         | Yes      | JSON that describes the authentication and other details |
|               |              |          |    for this provider.  The actual contents of this field |
|               |              |          |    can vary depending on type.                           |
+---------------+--------------+----------+----------------------------------------------------------+
| created\_at   | String       | No           The creation tinestamp for this provider.              |
+---------------+--------------+----------+----------------------------------------------------------+
| updated\_at   | String       | No           The last modification timestamp for this provider.     |
+---------------+--------------+----------+----------------------------------------------------------+

Implementation
--------------

Providers are implemented in 2 parts:

* An external service that contains all the logic required to
  interface with (or implement) the external system.
* A shim in the Digital Rebar core that talks to the external service.  The
  shim must be a subclass of Provider, and provide implementations of
  the 4 basic provider methods

The 4 Basic Provider Methods
~~~~~~~~~~~~~~~~~~~~~~~~~~~~

Every provider must implement 4 methods to allow Rebar to manage nodes
using it -- 1 to initialize the provider itself, and 3 for basic node
operations.  As the scope of the providers grows, the number and type
of methods they must implement will grow as well.  The methods are:

:register\_endpoint: Register a new Provider.  This must be a private method that will be
  called after a new Provider is created via the Provider API.  It
  accepts no parameters.

:create\_node: Create a new node on the provider.  This method will be called as
  part of the node creation via the Rebar API.  It accepts the node as
  its parameter.

:reboot\_node: Reboot the node.  It accepts the node as its parameter.

:delete\_node: Delete the node from the provider.  It accepts the node as its parameter.

In general, the shim that implements these methods should be as small
as possible, calling out to the external service to do most of the
work.  These methods should also be non-blocking to the extent
feasible -- these methods should start doing whatever is needed and
return, and the external service should call back into Rebar as
appropriate once the work is done.

Creating a new provider
^^^^^^^^^^^^^^^^^^^^^^^

The recommended way to do this is to:

1. Write a shim that is a subclass of the Provider model.  It should at a handle the 4 basic
   provider API calls that the core expects to call as part of the node lifecycle.  An example of a functional shim is `fog_provider.rb <https://github.com/digitalrebar/core/blob/develop/rails/app/models/fog_provider.rb>` in the core Rebar repo.

2. Write an external service that the shim should use to interface with (or implement) the external provider. A good working example is the `fogwrap service<https://github.com/rackn/deploy-fogwrap/tree/master/fogwrap>`.
