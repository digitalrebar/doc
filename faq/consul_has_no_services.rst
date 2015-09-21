No Consul Services after Digital Rebar Restart
==============================================

If you restarted Digital Rebar but there are Consul is not showing any services then it is possible that the Digital Rebar containers were not removed before restart.

#. Use ``docker-compose stop && docker-compose rm`` to reset the environment.
#. Then ``docker-compose up`` to start it again

   #. If you watch the output stream, you should be able to see log messages from all the containers.
  
Another possible cause is using an old URL for Consul.  Try to connect with only http://[server_ip]:8500.
