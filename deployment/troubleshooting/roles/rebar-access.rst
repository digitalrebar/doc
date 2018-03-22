
.. note:: WARNING WARNING WARNING:  This is the Digital Rebar v2 product documentation.  That product line is EOL as of September 2017.  Please refer to the new Digital Rebar Provision v3 documentation:  http:\/\/provision.readthedocs.io\/en\/tip\/README.html

rebar-access
============

.. _rebar-access:

Cannot Reach SSH Address due to VPC
-----------------------------------

:typical log message: ``ERROR: SecureShellHammer.run cannot find a reachable address for ...``
:cause: AWS: Rebar VPC is different from VPC/Subnet in Provider
:solution: Make sure that the VPC / Subnet you are using for the provider is the same as the one that you installed Rebar on.  This could happen if you have multiple VPC and the default is different than the one you picked on the quickstart.


Cannot Reach SSH Address due to Cloudwrap Failure
-------------------------------------------------

:typical log message: ``ERROR: SecureShellHammer.run cannot find a reachable address for ...``
:cause: Cloudwrap was not able to create a throwaway SSH ID for the Node
:solution: Look at `docker logs -f compose_cloudwrap_1` to make sure that the process is completed from that end, but it sounds like it is.  You should be able to see the short term "cloudwrap" SSH keys created in your keys list


Cannot Reach SSH Address due to unreachable SSH 
-----------------------------------------------

:typical log message: ``ERROR: SecureShellHammer.run cannot find a reachable address for ...``
:cause: Networking issues between Rebar Engine and Node
:solution: You can verify that rebar can SSH to the node's IP address from the `docker exec -it compose_rebar_api_1 bash` and then `su - rebar`.  From that account, you can validate SSH connectivity with the rebar keys to the target system.  This will allow you to validate connectivity.
