Development Guide
=================

Welcome to the amazing world of Digital Rebar!

This guide is targeted at individuals who wish to *contribute and extend*
Digital Rebar. You should review the architectural and operator
instructions as part of the learning process.

.. toctree::
   :maxdepth: 1
   :glob:
   
   contributing/contributing
   contributing/contributing-code
   contributing/mark
   contributing/workflow
   ui/README
   jigs/README
   sledgehammer/build_sledgehammer
   sledgehammer/dev-build-sledgehammer
   sledgehammer/sledgehammer-hooks
   smoketesting
   api/README

API
------------------

Our intention is to keep
the API documentation focused just on using the API and leave more it to
curious readers to review the model and principles areas.

Dev Environment
---------------

Our development environments include a *working* administrative server
for testing. It is very important in our process that developers are
able to run deployments in their environment as part of the testing
cycle.

While we have invested in BDD and system tests to catch core logic
errors, most changes require performing a deployment to test
correctness!

> Protip: You can enter the Rails Console from the host, using ``docker exec -it compose_rebar_api_1 /opt/digitalrebar/core/tools/rails-console.sh``.  This works for development and production!

Setting Rails Development Mode
------------------------------

Digital Rebar does not use use RAILS_ENV=development in the traditional way because most of our testing is targeted at doing real provisioning work that requires the production system.

If you have a need for development behavior (classes and views the refresh when code changes) then perform the following steps:

#. Deploy Digital Rebar in the normal way
#. From the host, create the ``dev.mode`` file in the digitalrebar home directory and restart the rebar_api contain

   ```touch ~/digitalrebar/dev.mode
   cd ~/digitalrebar/deploy/compose && docker-compose restart rebar_api
   ```

You may make any Rails configuration changes by created your own ``core/rails/config/environments/production.rb`` file.  Since we ignore ``production.rb`` you can leave your own customized version in place.
