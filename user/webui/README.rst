.. _user_guide:

Web UI Guide
============

This is the Digital Rebar Web Interface.

.. toctree::
  :maxdepth: 1
  :glob:

  login
  overview
  annealer
  monitor
  ready_state_wizard
  deployment
  nodes
  roles
  providers
  barclamps
  networks
  jigs
  groups
  hammers
  families

State Image Key
~~~~~~~~~~~~~~~

The follow table describes the states and icons used by Digital Rebar throughout the Web UI.

+--------------+------------------------+-----------------------------------------------------------+
| State        | Icon                   | Description                                               |
+==============+========================+===========================================================+
| Ready        | |Ready (image)|        | Updates applied, Stable                                   |
+--------------+------------------------+-----------------------------------------------------------+
| Error        | |Error (image)|        | Failed, Incomplete transition                             |
+--------------+------------------------+-----------------------------------------------------------+
| Blocked      | |Blocked (image)|      | Annealer waiting until all prereq's met                   |
+--------------+------------------------+-----------------------------------------------------------+
| Idle         | |Idle (image)|         | System not active                                         |
+--------------+------------------------+-----------------------------------------------------------+
| Off          | |Off (image)|          | Power is off. No activity possible                        |
+--------------+------------------------+-----------------------------------------------------------+
| Wait         | |Wait (image)|         | Todo action but power is off. Waiting until power is on   |
+--------------+------------------------+-----------------------------------------------------------+
| Proposed     | |Proposed (image)|     | Waiting on user input                                     |
+--------------+------------------------+-----------------------------------------------------------+
| Reserved     | |Reserved (image)|     | User hold on activity                                     |
+--------------+------------------------+-----------------------------------------------------------+
| To do        | |TODO (image)|         | All prereq's met but not Annealer not started yet         |
+--------------+------------------------+-----------------------------------------------------------+
| Transition   | |Transition (image)|   | Annealer sent work to Jig                                 |
+--------------+------------------------+-----------------------------------------------------------+


.. |Ready (image)| image:: /images/icons/led/active.png
.. |Error (image)| image:: /images/icons/led/error.png
.. |Blocked (image)| image:: /images/icons/led/blocked.png
.. |Idle (image)| image:: /images/icons/led/active.png
.. |Off (image)| image:: /images/icons/led/off.png
.. |Wait (image)| image:: /images/icons/led/wait.png
.. |Proposed (image)| image:: /images/icons/led/proposed.png
.. |Reserved (image)| image:: /images/icons/led/reserved.png
.. |TODO (image)| image:: /images/icons/led/todo.png
.. |Transition (image)| image:: /images/icons/led/transition.png
