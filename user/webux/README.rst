
.. note:: WARNING WARNING WARNING:  This is the Digital Rebar v2 product documentation.  The v2 version is EOL as of September 2017.  Please refer to the new Digital Rebar Provision v3 documentation:  http:\/\/provision.readthedocs.io\/en\/tip\/README.html

.. _web_ux_guide:

Web UX Guide
============

This is the Digital Rebar Web Experience.  Both the UX and the documentation are still under construction.

.. toctree::
  :maxdepth: 1
  :glob:

  login
  overview
  annealer
  deployment
  workload
  providers
  nodes
  profiles
  networks
  services
  provisioner
  access
  errors
  advanced/README

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
+--------------+------------------------+-----------------------------------------------------------+
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
