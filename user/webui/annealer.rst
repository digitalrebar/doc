.. index::
  pair: Web UI; Annealer

.. _ui_annealer:

Annealer
========

The Annealer page (/annealer) shows all the active node-roles (see :ref:`ui_roles`) in the system grouped by type with the most immediate types (error, process) at the top.  The Annealer can be reached via the radar icon in the top right.

.. image:: /images/screens/dr_annealier_monitor.png

For more on the function of the Annealer, see :ref:`simulated_annealing`.

Operation
---------

The Annealer page automatically refreshes every 15 seconds (adjustable in the top right corner).  As the system changes, node-role status is displayed for each role-role.  Clicking on a role will display additional information about the status of the role.  

For any roles in error, a retry button and retry-all button is provided.

