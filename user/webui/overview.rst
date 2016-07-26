.. _ui_overview:

Overview
========

The Overview page provides a quick view of system health.  Unlike most screens, it is designed to show the general functional status of the system instead of by-node or by-deployment status.

.. image:: /images/screens/dr_overview_startup.png

Operation
---------

The Overview page is read-only and automatically refreshes.  As the system changes, node-role status is displayed for each role-role.  If a single function has too many items to display individually, a count by type is shown instead.

If all the roles in a function are ready (as shown above), then the function is shown green.  If any function is in error then the function is red.  For other states, it will be yellow.

Developer Note
--------------

The classification of node-roles into function groups is determined by the "`layercake.json <https://github.com/digitalrebar/core/blob/develop/rails/config/layercake.json>`_" in the core\\rails\\config path.  Roles that have not been assigned are automatically added to the "application" layer.
