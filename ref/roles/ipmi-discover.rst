
.. note:: WARNING WARNING WARNING:  This is the Digital Rebar v2 product documentation.  The v2 version is EOL as of September 2017.  Please refer to the new Digital Rebar Provision v3 documentation:  http:\/\/provision.readthedocs.io\/en\/tip\/README.html

=============
ipmi-discover
=============

Description
===========
Discover and inventory the local IPMI controller

Documentation
=============

ipmi-discover is responsible for discovering and inventorying the local
IPMI controller for the system if one is present.  It tries to gather
information about the IPMI controller using ipmitool in-band communication, which
sidesteps the whole question about how you perform out-of-band discovery and
trying to guess the appropriate default usernames and passwords.

If we discover an IPMI controller, we perform a basic inventory of it and determine
what (if any) quirks the IPMI controller has (such as requiring a delay between commands,
whether one of the users is immutable, whether the channels used for network config
are messed up (and how), etc).
