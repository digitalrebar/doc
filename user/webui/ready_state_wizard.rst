.. _ui_ready_state:

Ready State Wizard
==================

Ready State is a Digital Rebar concept used to describe a node that has been prepared for further work.

.. image:: /images/screens/dr_ready_state_wizard.png

Operation
---------

The Ready State Wizard performs multiple steps for provisioning
discovered :ref:`ui_nodes` from a single screen. This convenience eliminates
several steps that are commonly performed together.

From the Ready State Wizard Screen:

  1. Name the deployment (network will be named the same as the deployment)
  #. Describe the network settings (this can be changed from the Networks page at a later date)
  #. Check the nodes to provisioned
  #. Select the o/s to be installed
  #. Accept the changes (this opens the deployment page)
  #. Commit the deployment to begin.

Change OS
---------

The OS can be altered after the wizard has run by clicking on the ``provisioner-os-install`` node role for the individual nodes (the blue wrench icon).

.. image:: /images/screens/dr_ready_state_change_os.png

Install note: The list will be limited to the available operating systems.  See the install guide to add more choices to the list.

Commit Deployment
-----------------

Digital Rebar will not start while the deployment is in the proposed status (user managed).  To release the deployment, ``commit`` the deployment by clicking the ``commit`` button.

.. image:: /images/screens/dr_ready_state_precommit.png


Running Install
---------------

Once the deployment has been committed, Digital Rebar will begin the install process automatically.

.. image:: /images/screens/dr_install_running.png
