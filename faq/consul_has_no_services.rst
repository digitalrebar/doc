
.. note:: WARNING WARNING WARNING:  This is the Digital Rebar v2 product documentation.  The v2 version is EOL as of September 2017.  Please refer to the new Digital Rebar Provision v3 documentation:  http:\/\/provision.readthedocs.io\/en\/tip\/README.html

.. index::
	Consul; No Service

.. _faq_consul:

Why is There No Consul Service After Digital Rebar Restarts?
============================================================

If Digital Rebar has been restarted but the Consul is not showing any services, it is possible that the Digital Rebar containers were not removed before restart.

#. Use ``docker-compose stop && docker-compose rm`` to reset the environment.
#. Then ``docker-compose up`` to start it again

   - Log messages from all the containers will be visible in the output stream.
  
Another possible cause is using an old URL for Consul.  Try to connect with only http://[server_ip]:8500.
