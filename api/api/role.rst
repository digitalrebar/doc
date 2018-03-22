
.. note:: WARNING WARNING WARNING:  This is the Digital Rebar v2 product documentation.  That product line is EOL as of September 2017.  Please refer to the new Digital Rebar Provision v3 documentation:  http:\/\/provision.readthedocs.io\/en\/tip\/README.html

.. index::
  pair: Role; API

.. _api_role:

Role APIs
~~~~~~~~~

Roles are a core data type in Digital Rebar.  They are used to define
services that Digital Rebar deploys in the environment.

    Role names are globally unique.  This restriction may be related in
    the future

Role Types
^^^^^^^^^^

Digital Rebar allows Barclamp creators to override the default Role
behavior.  This is a very import extension point for Digital Rebar
because custom Role behaviors are essential to many orchestration
situations.

If no override is provided, Digital Rebar will use the Digital
Rebar::Role class.

A role specific override can be created using the name of the
barclamp-role to create the class in the Barclamp model name space.  For
example, a role called test-admin should be created as
BarclampTest::Admin (or app/models/barclamp\_test/admin.rb).  When the
role is imported, Digital Rebar will automatically use this type if it
has been defined.

A Barclamp specific override can be created using the name of the
barclamp and the class role.  If present, this class will be used if no
specific role class has been provided.  This is very useful for barclamps
that create roles dynamically such as the network barclamp.  For example,
Digital Rebar will use the BarclampNetwork::Role (or
app/models/barclamp\_network/role.rb) class when new Network roles are
added.  This allows Barclamp creators to add custom event handling
without knowing the name of the roles in advance.

    This is also related to how Role Events are handled.

API Actions
^^^^^^^^^^^

+----------+-------------------------------------------+--------------------------------------------------------+
| Verb     | URL                                       | Comments                                               |
+==========+===========================================+========================================================+
| GET      | api/v2/roles                              | List                                                   |
+----------+-------------------------------------------+--------------------------------------------------------+
| GET      | api/v2/roles/:id                          | Specific Item                                          |
+----------+-------------------------------------------+--------------------------------------------------------+
| GET      | /api/v2/roles/[:role\_id]/attribs         | List Attribs for a specific role                       |
+----------+-------------------------------------------+--------------------------------------------------------+
| GET      | /api/v2/roles/[:role\_id]/attribs/[:id]   | Show Attrib (including value) for a specific Role      |
+----------+-------------------------------------------+--------------------------------------------------------+
| PUT      | /api/v2/roles/[:role\_id]/attribs/[:id]   | Update Attrib                                          |
+----------+-------------------------------------------+--------------------------------------------------------+
| PUT      | -                                         | NOT SUPPORTED / managed during import only             |
+----------+-------------------------------------------+--------------------------------------------------------+
| POST     | -                                         | NOT SUPPORTED / roles are only created during import   |
+----------+-------------------------------------------+--------------------------------------------------------+
| DELETE   | -                                         | NOT SUPPORTED                                          |
+----------+-------------------------------------------+--------------------------------------------------------+

Role Events (triggered on NodeRole state changes)
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

The Role model has a series of events (Self.on\_[STATE]) that are called
when any NodeRole changes state.  This is a designed override point where
Barclamp Roles can add functionality into the Digital Rebar Annealer
engine.  This functionality is added when a Barclamp defines it's own
Role definitions (Barclamp[Name]::[Role]).  If there is no override, then
the default behavior is used.

There is a matching event for each NodeRole state.  The event is called
when the NodeRole enters that state.  The purpose of this function is to
enable Barclamp creators to leverage information available to Digital
Rebar within the Annealer operation including before user editing
(Proposed) or system error (Error) states.

JSON fields
-----------

+----------------+----------------+------------+-------------------------+
| Attribute      | Type           | Settable   | Note                    |
+================+================+============+=========================+
| Description    | String         | Yes        |                         |
+----------------+----------------+------------+-------------------------+
| Name           | String         | Yes        |                         |
+----------------+----------------+------------+-------------------------+
| Created\_at    | String         | No         | Unicode - date format   |
+----------------+----------------+------------+-------------------------+
| Updated\_at    | String         | No         | Unicode - date format   |
+----------------+----------------+------------+-------------------------+
| Server         | Boolean        | Yes        |                         |
+----------------+----------------+------------+-------------------------+
| Bootstrap      | Boolean        | Yes        |                         |
+----------------+----------------+------------+-------------------------+
| Library        | Boolean        | Yes        |                         |
+----------------+----------------+------------+-------------------------+
| Barclamp\_id   | Internal Ref   | ??         | Actually an Int         |
+----------------+----------------+------------+-------------------------+
| Cluster        | Boolean        | Yes        |                         |
+----------------+----------------+------------+-------------------------+
| Implicit       | Boolean        | Yes        |                         |
+----------------+----------------+------------+-------------------------+
| Template       | String         | Yes        | Another json blob       |
+----------------+----------------+------------+-------------------------+
| Jig Name       | String         | Yes        |                         |
+----------------+----------------+------------+-------------------------+
| Destructive    | Boolean        | Yes        |                         |
+----------------+----------------+------------+-------------------------+
| Service        | Boolean        | Yes        |                         |
+----------------+----------------+------------+-------------------------+
| id             | Internal Ref   | ??         | Actually an Int         |
+----------------+----------------+------------+-------------------------+
| Discovery      | Boolean        | Yes        |                         |
+----------------+----------------+------------+-------------------------+

Structure of the template JSON (from an example)
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

The template structure is multi-layered - in the table assume that the
lines following a 'blob' are the subsidiary structure

+-----------+-------------+
| Name      | Value       |
+===========+=============+
| Ceph      | json blob   |
+-----------+-------------+
| config    | json blob   |
+-----------+-------------+
| osd       | json blob   |
+-----------+-------------+
| journal   | file        |
+-----------+-------------+
| encrypt   | False       |
+-----------+-------------+
| fstype    | xfs         |
+-----------+-------------+

