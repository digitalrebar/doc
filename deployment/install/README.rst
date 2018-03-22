
.. note:: WARNING WARNING WARNING:  This is the Digital Rebar v2 product documentation.  That product line is EOL as of September 2017.  Please refer to the new Digital Rebar Provision v3 documentation:  http:\/\/provision.readthedocs.io\/en\/tip\/README.html


.. index::
  pair: Admin Node; Deployment

.. _install:

Deploy Digital Rebar Admin Node
===============================

At this point :ref:`initial_install_setup` and :ref:`dg_config` should have been completed.

Tool Setup
----------

.. toctree::
  :maxdepth: 1
  :glob:

  dr_info
  cli_setup

Once the tools are setup, :ref:`workloads_guide` can be used to deploy an :ref:`arch_other_systems` and a workload at the same time.  This can be faster for initial set up, but it can also limit a multi-use deployment.  The workload scripts can also reference an already installed admin node as well.

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
  raid-bios
