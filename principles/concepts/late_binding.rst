
.. note:: WARNING WARNING WARNING:  This is the Digital Rebar v2 product documentation.  The v2 version is EOL as of September 2017.  Please refer to the new Digital Rebar Provision v3 documentation:  http:\/\/provision.readthedocs.io\/en\/tip\/README.html

.. _late_binding:

Ops Late Binding
================

In terms of computer science languages, late binding describes a class
of 4th generation languages that do not require programmers to know all
the details of the information they will store until the data is
actually stored.  Historically, computers required very exact and
prescriptive data models, but later generation languages embraced a more
flexible binding.

Ops is fluid and situational.

Many DevOps toolings leverage eventual consistency to create stable
deployments.  This iterative approach assumes that repeated attempts of
executing the same idemnepotent scripts do deliver this result.  However,
they do not deliver predictable upgrades in situations where there
are circular dependencies to resolve.

It is also not realistic to predict the exact configuration of a system in
advance because the operational requirements recursively impact how the infrastructure is configured, ops environments must be highly dynamic, and resilience requires configurations to be tolerant of change.

The specifics of the deployment allow for more complex upgrades where the steps cannot be determined in advance.
