.. _ux_annealer:

The Annealer
~~~~~~~~~~~~

When opened, the Annealer shows the progress of node role deployment. Active node roles are grouped by type, with the most immediate types (error, process) at the top. The Annealer can be reached via the radar icon in the top right.


.. image:: /images/screens/webux/annealer.png


* Error shows all of the node roles in error.
* Process shows all of the node roles which are being processed.
* Todo shows nodes that are about to be processed.
* Queue shows nodes that are waiting to enter Todo.

**Note**: Error has a retry button that will send all erroneous node roles back to the queue.

Operation
---------

The Annealer page automatically refreshes every 15 seconds (adjustable in the top right corner).  As the system changes, node role status is updated.  Clicking on a role will display additional information about the status of the role.

For more on the function of the Annealer, see :ref:`simulated_annealing`.



