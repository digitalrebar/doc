.. _dev_guide:

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

*Protip:* It is possible to enter the Rails Console from the host using ``docker exec -it compose_rebar_api_1 /opt/digitalrebar/core/tools/rails-console.sh``.  This works for development and production!

Setting Rails Development Mode
------------------------------

Digital Rebar does not use RAILS_ENV= development in the traditional way because most of our testing is targeted at doing real provisioning work that requires the production system.

If there is a need for development behavior (classes and views that refresh when code changes), perform the following steps:

#. Deploy Digital Rebar normally.
#. From the host, create the ``dev.mode`` file in the digitalrebar home directory and restart the rebar_api container::

      touch ~/digitalrebar/dev.mode
      cd ~/digitalrebar/deploy/compose && docker-compose restart rebar_api

Any Rails configuration changes may be made by creating a ``core/rails/config/environments/production.rb`` file to work off of.  Since we ignore ``production.rb`` the customized version can be left in place.
