.. _dev_guide:

Development Guide
=================

Welcome to the amazing world of Digital Rebar!

This guide is targeted at individuals who wish to *contribute and extend*
Digital Rebar. Please review the architectural and operator
instructions as part of the learning process.

.. toctree::
   :maxdepth: 1
   :glob:
   
   contributing/contributing
   contributing/contributing-code
   contributing/contributing-docs
   contributing/mark
   dev_env/README
   ui/README
   jigs/README
   sledgehammer/build_sledgehammer
   directory-layout

Dev Environment
---------------

Our development environments include a *working* administrative server
for testing. It is very important in our process that developers are
able to run deployments in their environment as part of the testing
cycle.

> Protip: The Rails Console can be entered from the host, using ``docker exec -it compose_rebar_api_1 /opt/digitalrebar/core/tools/rails-console.sh``.  This works for development and production!

Setting Rails Development Mode
------------------------------

Digital Rebar does not use use RAILS_ENV=development in the traditional way because most of our testing is targeted at doing real provisioning work that requires the production system.

If development behavior is required (classes and views the refresh when code changes) then perform the following steps:

#. Deploy Digital Rebar in the normal way
#. From the host, create the ``dev.mode`` file in the digitalrebar home directory and restart the rebar_api contain

   ```touch ~/digitalrebar/dev.mode
   cd ~/digitalrebar/deploy/compose && docker-compose restart rebar_api
   ```

Rails configuration changes can be made by created a personal ``core/rails/config/environments/production.rb`` file.  Please be certain to leave ``production.rb`` out of any pull requests. 