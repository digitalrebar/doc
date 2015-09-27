Development Guide
=================

Welcome to the amazing world of Digital Rebar!

This guide is targeted at individuals who wish to *contribute and extend*
Digital Rebar. You should review the architectural and operator
instructions as part of the learning process.

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

Setting Rails Development Mode
------------------------------

Digital Rebar does not use use RAILS_ENV=development in the traditional way because most of our testing is targeted at doing real provisioning work that requires the production system.

If you have a need for development behavior (classes and views the refresh when code changes) then perform the following steps:

#. Deploy Digital Rebar in the normal way
#. ``cp core/rails/config/environments/development.rb core/rails/config/environments/production.rb``
#.  delete the production setting from ``core/rails/config/application.rb`` (this is not be required in future)
#. ``docker exec -it compose_rebar_api_1 bash``
#. ``touch /tmp/development.txt``
#. ``service rebar restart``

You may make any Rails configuration changes desired in the same way.  Since we ignore ``production.rb`` you can leave your own customized version in place.

