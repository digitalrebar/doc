.. index::
  pair: Developer; Dev Mode

.. _dev_guide_dev_env:

Dev Environment
---------------

Our development environments include a *working* administrative server
for testing. It is very important in our process that developers are
able to run deployments in their environment as part of the testing
cycle.

Protip: The Rails Console can be entered from the host with ``docker exec -it compose_rebar_api_1 /opt/digitalrebar/core/tools/rails-console.sh``.


.. toctree::
  :maxdepth: 1
  
  docker-cheats
  rails-dev
  docker_admin
  kvm-slaves

  *