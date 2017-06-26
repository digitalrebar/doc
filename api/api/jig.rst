.. index::
  pair: Jig; API

.. _api_jig:

Jig (aka CMDB interface) APIs
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

Jigs are the interface between Digital Rebar and doing work in the
infrastructure.

System Jigs
^^^^^^^^^^^

Digital Rebar has three built-in jigs

-  Script - uses SSH to perform operations on nodes.  This is used for
   bootstrapping actions that install the agents for other Jigs.  Not
   activated in development mode.
-  Noop (no operation) - takes internal actions in Digital Rebar only.
   Used when database updates or coordination points are needed that
   have no external action.
-  Test - used by the test infrastructure to validate Digital Rebar
   logic when no physical infrastructure is available.  Not activated in
   production mode.

API Actions
^^^^^^^^^^^

+-----------+-------------------------+-----------------------------------+
| Verb      | URL                     | Comments                          |
+===========+=========================+===================================+
| GET       | api/v2/jigs             | List                              |
+-----------+-------------------------+-----------------------------------+
| GET       | api/v2/jigs/:id         | Specific Item                     |
+-----------+-------------------------+-----------------------------------+
| PUT       | api/v2/jigs/:id         | Update Item                       |
+-----------+-------------------------+-----------------------------------+
| POST      | api/v2/jigs             | Create Item                       |
+-----------+-------------------------+-----------------------------------+
| DELETE    | api/v2/jigs/:id         | Delete Item                       |
+-----------+-------------------------+-----------------------------------+
| PUT       | api/v2/jigs/:id/flush   | (optional) Clear downloaded cache |
+-----------+-------------------------+-----------------------------------+
| VARIOUS   | api/v2/jigs/:id/extra   | Special Ops                       |
+-----------+-------------------------+-----------------------------------+

**Note**: Flush is not implemented in all Jigs.  The Ansible Playbook jig does implement this feature.
