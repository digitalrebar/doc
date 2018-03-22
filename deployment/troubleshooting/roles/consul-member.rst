
.. note:: WARNING WARNING WARNING:  This is the Digital Rebar v2 product documentation.  That product line is EOL as of September 2017.  Please refer to the new Digital Rebar Provision v3 documentation:  http:\/\/provision.readthedocs.io\/en\/tip\/README.html

Consul Member Errors
====================

Restart Consul Returned 6
-------------------------

:typical log message: ``Error executing action `restart` on resource 'service[consul]'`` or ``/bin/systemctl restart consul returned 6, expected 0``
:cause: This is an intermittent timing issue
:solution: Often a retry is sufficient.  If retry fails, it may be a larger networking issue
