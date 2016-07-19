.. _install:

Deploy Digital Rebar Admin Node
===============================

At this point :ref:`initial_install_setup` and :ref:`dg_config` should haved been completed.

Tool Setup
----------

.. toctree::
  :maxdepth: 1
  :glob:

  dr_info
  cli_setup

Once the tools are setup, :ref:`workloads_guide` can be used to deploy an admin node and a workload at the same time.  This can be faster for initial bring up, but can limit a multi-use deployment.  The workload scripts can also reference an already installed admin node as well.

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
  providers

Post Deployment Actions
-----------------------

Sometimes there are addtional sets that need to be done to complete the deployment.

.. toctree::
  :maxdepth: 1
  :glob:

  attaching-to-bmc

