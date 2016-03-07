Configuration Managers (aka Jigs)
=================================

Jigs are the interface between Digital Rebar and external work that
needs to be done.

Digital Rebar provides a pluggable model for interacting with nodes and
other datacetner infrastructure components such as switches, power
controllers, failover controllers, etc. Each differing *configuration
manager* has its own interfaces and control methods. Digital Rebar
provides a defined API for the *configuration managers* needed to
control and manage a collection of machines and systems.

For convenience the Digital Rebar method for initiating and controlling
a node-role state transition operation through a particular *control
manager* is via a **Jig**. A **Jig** provides a consistent interface for
Digital Rebar state transition vectors. State transition vectors operate
within the context of a predefined dependency graph. The collection of
Digital Rebar **Jigs** provide a platform-agnostic and operationally
neutral method for initiating, monitoring, and completing a node-role
state transition.

Digital Rebar must have 1 or more Jigs that preform the work of node-role state transition operations, known as **Jobs**.

For initial Digital Rebar work, the primary **Jigs** inclide:
-------------------------------------------------------------

.. toctree::
   :maxdepth: 1
   :glob:
   
   *

JIG semantic standard operations:
---------------------------------

1. A jig can create roles for operation
2. A jig can set attributes for operations

The Digital Rebar roadmap includes provision to use a **Puppet** jig.
The **Puppet JIG** will include both front0-end driver as well as a
**Puppet-client** capability.

For testing, Digital Rebar provides a Test Jig that is included in the
core Digital Rebar barclamp.

Schema
~~~~~~

Jig names have a limited character set. They can only include
alphanumeric characters and underscore (\_). They cannot start with
underscore.

Inbound path
~~~~~~~~~~~~

The jig can read data from the system and store it into attribute
collection via JSON databags.

User Data
^^^^^^^^^

More information to follow.

System Data
^^^^^^^^^^^

More information to follow.

Outbound path
~~~~~~~~~~~~~

More information to follow.

Methods
~~~~~~~

Each jig overrides the following core methods in Digital Rebar:

Create Node
^^^^^^^^^^^

Handles when a node is added to the Digital Rebar DB. Allows the jig to
make approporate entries in independant databases

Delete Node
^^^^^^^^^^^

Handles when a node is removed from the Digital Rebar DB. Allows the jig
to remove entries from its database

Run (input is list of Tacks)
^^^^^^^^^^^^^^^^^^^^^^^^^^^^

