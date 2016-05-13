.. _install:

Deploy Digital Rebar Admin Node
===============================

At this point, you should have done, :ref:`initial_install_setup`, and done any :ref:`dg_config`.

Tool Setup
----------

.. toctree::
  :maxdepth: 1
  :glob:

  dr_info
  cli_setup

Once the tools are setup, you could use the :ref:`dg_workloads` instead to deploy an admin node and a workload at the 
same time.  This can be faster for initial bring up, but can limit a multi-use deployment.  The workload scripts can also 
reference an already installed admin node as well.

Specific Environments
---------------------

.. toctree::
  :maxdepth: 1
  :glob:

  linux
  packet
  aws
  google
  vagrant
  ansible

Post Deployment Actions
-----------------------

Sometimes there are addtional sets that need to be done to complete the deployment.

.. toctree::
  :maxdepth: 1
  :glob:

  attaching-to-bmc

