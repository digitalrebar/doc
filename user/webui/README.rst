.. index::
  pair: Web UI; Guide

.. _web_user_guide:

Web UI Guide
============

This is the Digital Rebar Web Interface.

.. toctree::
  :maxdepth: 1
  :glob:

  login
  annealer
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

.. index::
  Web UI; State/Image Key

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
| Queue        | |Queue (image)|        | Annealer waiting until all prereq's met                   |
+--------------+------------------------
+-----------------------------------------------------------+
| Off          | |Off (image)|          | Power is off. No activity possible                        |
+--------------+------------------------+-----------------------------------------------------------+
| Proposed     | |Proposed (image)|     | Waiting on user input                                     |
+--------------+------------------------+-----------------------------------------------------------+
| Reserved     | |Reserved (image)|     | User hold on activity                                     |
+--------------+------------------------+-----------------------------------------------------------+
| To do        | |TODO (image)|         | All prereq's met but not Annealer not started yet         |
+--------------+------------------------+-----------------------------------------------------------+
| Process      | |Process (image)|      | Annealer sent work to Jig                                 |
+--------------+------------------------+-----------------------------------------------------------+


.. |Ready (image)| image:: /images/icons/led/ready.png
.. |Error (image)| image:: /images/icons/led/error.png
.. |Queue (image)| image:: /images/icons/led/queue.png
.. |Off (image)| image:: /images/icons/led/off.png
.. |Proposed (image)| image:: /images/icons/led/proposed.png
.. |Reserved (image)| image:: /images/icons/led/reserved.png
.. |TODO (image)| image:: /images/icons/led/todo.png
.. |Process (image)| image:: /images/icons/led/process.png
