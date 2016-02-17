Consul Member Errors
====================

Restart Consul Returned 6
-------------------------

``Error executing action `restart` on resource 'service[consul]'``
and 
``/bin/systemctl restart consul returned 6, expected 0``

This is an intermittent timing issue, please retry the action and it should resolve.
