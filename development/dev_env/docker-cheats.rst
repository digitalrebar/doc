.. index::
	Development; Docker Cheats
	Docker; Docker Cheats

.. _dev_guide_docker:

Docker Cheats for Developers
----------------------------


While `docker exec -it compose_rebar_api_1 bash` can always be used to get into the API container, here are some handy cheats that can be used to do routine tasks inside the API container:

* Tail Logs: ``docker exec -it compose_rebar_api_1 tail -f /var/log/rebar/production.log``
* Open Rails Console (to test models & database direct): ``docker exec -it compose_rebar_api_1 /opt/digitalrebar/core/bin/rebar_console``
* Use the CLI: ``docker exec -it compose_rebar_api_1 rebar ping``
* Reimport Barclamps: ``rebar -E "https://127.0.0.1:3000" -U "rebar" -P "rebar1" barclamps import /opt/digitalrebar/[workload]/rebar.yml``